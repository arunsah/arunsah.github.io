# Database architecture in Microservices
📅 [2020-06-07](https://arunsah.github.io/meta/changelog#2020-06-07) 🖊️ [@arunsah](https://github.com/arunsah) 🧭 [Pune, India](https://en.wikipedia.org/wiki/Hinjawadi)

---

## CAP Theorem
- CAP (Consistency/Availability/Partition Tolerance) Theorem:
	- For distributed system, it is impossible to provide 3/3 grantees.
	- For networked system, Partition Tolerance is not optional, we have to choose from Consistency and Availability.
	- Consistency: every read request, received most recent writes/error.
	- Availability: every request, receives non-error response (response may not be most recent write).
	- Partition Tolerance: system continuous to operate despite arbitrary number of messages being dropped/delayed by network between nodes.


## Managing inter-service transactions
- For transactions spanning services:
	- use Saga pattern
- For queries spanning services:
	- use API composition.
	- use CQRS
  
  
## Data storage and management in Microservice 

### Database per Service Pattern
- A service transactions only involve its database.
- Each ms persist data privately and accessible only via API.
- Db is part of ms implementation.
- One db for each service is not required as db can be used as:
	1. Private tables per service: 
		1. sets of tables accessed by specific ms.
		2. Lowest overhead.
	2. Schema per service: 
		1. each service has a db schema that’s private to it.
		2. Lowest overhead.
		3. Makes ownership clear.
	3. Db server per service: 
		1. each service has its own db server.
		2. High throughput services might need their own db server.
- Each service may have separate db user id and uses db access control mechanism (GRANTS).
- Pros:
	- Services are loosely coupled.
	- Each services can uses db best suited for its business logic.
		- ElasticSearch for text searches.
		- Neo4j for social graph.
- Cons:
	- Distributed transactions/Business logic comprising multiple services is complex due to CAP theorem.
	- NoSQL db doesn’t support distributes transactions.
	- Join over multiple db/tables are complex, loose performances.
	- Expertise in maintaining different type of db.



### Shared database
- different services can access data from same db.
- it required providing same permission levels for the services.
- Eg. Order service and Customer service maintains their tables in same db and can access data owned by other service using local ACID (Atomicity, Consistency, Isolation, Durability; set of properties of db transactions intended to guarantee validity even in the event of error/power failure/etc) transactions.

```sql
begin transaction
...
select order_total from order where cid=?;
...
select credit_limit from customer where cid=?;
...
insert into order ...
...
-- db will ensures that credit_limit will not be exceeded even in case of simultaneous transactions for same customer
commit transaction
```
- Pros:
	- ACID transactions to enforce data consistency.
	- single db is easy to operate/maintain.
- Cons:
	- development time coupling: tight coupling of tables will slow down changes of services and required coordination.
	- runtime coupling: any services locking table will block any other operations by different services.
	- db/configuration/throughputs requirement of each services might be different.


### Saga
- Saga is sequence of local transactions.
- Each business transaction that spans multiple services is implemented as saga.
- Each local transactions updated db then publishes a message or trigger event for next local transaction in saga.
- If a local transaction fails because a business rule is violated then saga executes a series of **compensating transactions** that undo the changes made by preceding local transactions.
- Use sagas instead of 2PC (2 phase commit).
- Ways to coordinate sagas:
	- Choreography: 
		- each local transaction publishes domain events that trigger local transactions in other services.
			- Order service created an order `order.status=pending` and publishes `order-created-event`.
			- Customer services subscribed to `order-topic`, receives the events trying to reserve credit for that order. It publishes `credit-reserved-event` or `credit-limit-exceeded-event`and publishes to `customer-topic`.
			- Order service subscribed to `customer-topic`, receives the event and changes the order’s status to `order.status=approved` or `order.status=cancelled`.
	- Orchestration:
		- orchestrator/object tells the participants what local transactions to execute.
			- Order service created an order `order.status=pending` and creates `CreateOrderSega`.
			- `CreateOrderSega` sends a `ReserveCredit` command to Customer service.
			- Customer service attempts to reserve credit for the order and response `credit-reserved` or `credit-limit-exceeded`.
			- `CreateOrderSega` receives the reply and either `ApproveOrder` or `RejectOrder` command to Order service. 
			- Order service changes the order’s status to `order.status=approved` or `order.status=cancelled` based on `CreateOrderSega` command.
- Pros:
	- enables application to maintain data consistency across multiple services without distributed transactions.
- Cons:
	- programming model is complex.
		- Eg. each forward transaction must have compensating transaction to undo changes made on earlier saga.
	- to be reliable, service must automatically update db and publishes message/event. It cannot use traditional mechanism of distributed transaction that spans db and message broker, it can use patterns such as API Composition, CQRS, Domain Event or Event sourcing.


---

### API Composition
- Used Database per Service Pattern, joins are difficult.
- Application performs the join rather than db.
	- Eg. service or API gateway can retrieve `one_cid => select cid from customer where email='tom@example.com'` and then `list_oid => select * from order where cid=one_cid`
- implement a query by defining an API composer.
	- It invokes the services owning the table and performs in-memory join.
- Pros:
	- simple to implement.
- Cons:
	- may be inefficient for large dataset.



### CQRS
- Used Database per Service Pattern, joins are difficult.
- Command Query Responsibility Segregation 
- maintain one/more materialised views that contain data from multiple services.
- views (read only replica) are kept by services that subscribe to domain events that each services publishes when it updated its data.
	- Eg. each services can maintain a read-only copy of required tables (shared tables) owned by other services. Whenever there is change in data on original table then the owner service will publishes update-event or created-event for that table on a message broker (such as Kafka). The subscribed service will update its internal copy accordingly. Further, subscribed service can decide to keep normalised or denormalised copy of the table.
	- Eg. Suppose there are two services Customer service and Order service. Each services have their sets of tables. The services have subscribed to Kafka topics.
		- Whenever there is any changes in customer details (update/insert/delete), customer service will publishes a notification event `customer-event` over Kafka `customer-topic`.
		- Suppose, Order service maintains internal copy of customer table and subscribed to `customer-topic` and handle `customer-event` to update/insert/delete its own copy of customer table data.
- Pros:
	- support multiple denormalised views (scalable/performant)
	- improved separation of concerns (simpler command and query models)
	- easy for event sourced architecture.
- Cons:
	- code/data duplication
	- replication lag/eventual consistent views.
	- increased complexity (require event sourcing architecture) 

---

### Domain Event
- derived from Domain Driven Design (DDD)
- business logic are organised as collection of DDD aggregates that emit domain events when they create/update data.
- service publishes events when it update its data.
	- require to update CQRS view.
	- require if service is participating in choreography-based-saga which uses events for coordinations.


### Event sourcing
- Used Database per Service Pattern, joins are difficult.
- not feasible to use distributed transaction that spans the db and message broker to automatically update db and publishes events.
- Service command needs to update db and send message/events in atomic manner in order to avoid data inconsistencies and bugs.
	- service is participating in orchestration-based-saga needs to update db and send message/event.
	- service publishes a domain event must atomically update an aggregated an publishes an event.
- It persists state of business entity (order or customer as sequence of state changing events).
	- whenever state of business entity changes, a new event is appended to list of events.
	- saving an event in a single operation is inherently atomic.
	- application reconstructs an entity’s current state by replying the events.
- applications persist events in an event store (db/log).
	- event store have API for adding/retrieving an entity’s events, for subscribing topics.
	- event store also behaves like a message broker.
	- to optimise loading, an application can periodically save a snapshot of an entity’s current state.
	- to reconstruct current state, application finds most recent snapshot and the events that have occurred since that snapshot leads to few events to replay.
- Framework/Infrastructure:
	- Kafka is a message broker and perhaps can be used as event store.
	- Eventuate focuses on Event Sourcing and event publication. 
	- Axon Framework and Axon Server (Enterprise) for event-driven microservices.
- Eg. Instead of storing current state of each order in ORDER Table, Order service add event/find event and persist each Order as a sequence of events:
	- In event store; `OrderCreated`, `OrderApproved`…`OrderShipped`.
	- Customer service subscribe to events and update its own state.

- Pros:
	- solves one of key problems in implementing an event-driven architecture and makes it possible to reliably publish events whenever state changes.
	- avoids object-relational impedance mismatch problem by storing events rather than domain objects.
	- reliable audit log of changes made to business entity.
	- temporal queries
	- business logic consists of loosely coupled business entities that exchanges events.
- Cons:
	- data is difficult to queries since it requires typical queries to reconstruct the sate of business entities.
		- application must use CQRS to implement queries, thus applications must handle eventually consistent data.


> Axon’s focus is much more on the abstraction of messaging, where messaging is both Commands, Events and (in a later stage also) Queries. It provides annotations to demarcate Event and Command handlers. It also allows you to design your entities in a way that keeps it decoupled from the framework’s internals. This abstraction allows you to “plug in" any database you would like to use as Event Store. Axon provides support for JPA, JDBC and MongoDB out of the box. As far as I can tell, Eventuate provides its own event store implementation. [cqrs - Axon Framework vs Eventuate comparison - Stack Overflow](https://stackoverflow.com/a/43201503)


### References:

- [7 Database Patterns for Microservices Architecture - YouTube](https://www.youtube.com/watch?v=a_XMsSNdUQA&t=305s)
- [Domain-driven design - Wikipedia](https://en.wikipedia.org/wiki/Domain-driven_design)
- [Sagas](https://microservices.io/patterns/data/saga.html)
- [Eventuate](https://eventuate.io/)
- [Eventuate example applications](https://eventuate.io/exampleapps.html#:~:text=There%20are%20numerous%20example%20applications,architecture%20using%20choreography%2Dbased%20sagas.&text=FTGO%20application%20%2D%20the%20example%20application%20for%20Chris%20Richardson's%20Microservices%20patterns%20book)
- [cqrs - Axon Framework vs Eventuate comparison - Stack Overflow](https://stackoverflow.com/questions/43136291/axon-framework-vs-eventuate-comparison)
- https://axoniq.io/
