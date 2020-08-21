# Spring Data JPA
## ManyToMany <-> ManyToMany and ManyToMany <-> OneToMany
📅 [2020-08-21](https://arunsah.github.io/meta/changelog#2020-08-21) 🖊️ [@arunsah](https://github.com/arunsah) 🧭 [Gopalganj, India](https://en.wikipedia.org/wiki/Gopalganj,_Bihar)

---

##### Relationship:

```java

	// * Member can be part of 1 House
	// Member.java
  @ManyToOne
  @JsonIgnore
  private House house;

  public void addHouse(House house) {
    this.house = house;
    house.addMember(this);
  }

	// 1 House can have * Member
	// House.java
  @OneToMany(mappedBy = "house", cascade = CascadeType.ALL, orphanRemoval = true)
  private List<Member> members = new ArrayList<>();


	// * Member can have * Activities
	// Member.java
  @ManyToMany
  @JoinTable(name = "MEMBER_ACTIVITY", joinColumns = @JoinColumn(name = "MEMBER_ID", referencedColumnName = "ID"),
          inverseJoinColumns = @JoinColumn(name = "ACTIVITY_ID", referencedColumnName = "ID"))
  private List<Activity> activities = new ArrayList<>();

  @Transient
  public List<String> getActivityName() {
    return this.activities.stream().map(a -> a.getName()).collect(Collectors.toList());
  }

  public void addActivity(Activity... activities) {
    for (Activity activity : activities) {
      this.activities.add(activity);
      activity.addMember(this);
    }
  }

	// * Avtivites can be followed by * Member
	// Activity.java
  @ManyToMany(mappedBy = "activities")
  private List<Member> members = new ArrayList<>();

  @Transient
  public List<String> getMembersName() {
    return this.members.stream().map(m -> m.getName()).collect(Collectors.toList());
  }

  public void addMember(Member member) {
    this.members.add(member);
  }
```

##### Result

```shell

# all houses
House [id=6, name=Gryffindor, members=15, memberName=[Albus Dumbledore, Harry Potter, Minerva McGonagall, Hermione Granger, Ron Weasley, Albus Dumbledore, Albus Dumbledore, Harry Potter, Harry Potter, Minerva McGonagall, Minerva McGonagall, Hermione Granger, Hermione Granger, Ron Weasley, Ron Weasley]]
House [id=7, name=Hufflepuff, members=3, memberName=[Hengist of Woodcroft, Newt Scamander, Artemisia Lufkin]]
House [id=8, name=Ravenclaw, members=4, memberName=[Luna Lovegood, Gilderoy Lockheart, Ignatia Wildsmith, Garrick Ollivander]]
House [id=9, name=Slytherin, members=3, memberName=[Tom Riddle, Bellatrix Black, Draco Malfoy]]

# all activities
Activity(id=1, name=Eating, members=[Member [id=13, name=Ron Weasley, house=House [id=6, name=Gryffindor, members=15, memberName=[Albus Dumbledore, Harry Potter, Minerva McGonagall, Hermione Granger, Ron Weasley, Albus Dumbledore, Albus Dumbledore, Harry Potter, Harry Potter, Minerva McGonagall, Minerva McGonagall, Hermione Granger, Hermione Granger, Ron Weasley, Ron Weasley]], activities=[Eating, Playing]]])
Activity(id=2, name=Playing, members=[Member [id=13, name=Ron Weasley, house=House [id=6, name=Gryffindor, members=15, memberName=[Albus Dumbledore, Harry Potter, Minerva McGonagall, Hermione Granger, Ron Weasley, Albus Dumbledore, Albus Dumbledore, Harry Potter, Harry Potter, Minerva McGonagall, Minerva McGonagall, Hermione Granger, Hermione Granger, Ron Weasley, Ron Weasley]], activities=[Eating, Playing]]])
Activity(id=3, name=Teaching, members=[Member [id=14, name=Hermione Granger, house=House [id=6, name=Gryffindor, members=15, memberName=[Albus Dumbledore, Harry Potter, Minerva McGonagall, Hermione Granger, Ron Weasley, Albus Dumbledore, Albus Dumbledore, Harry Potter, Harry Potter, Minerva McGonagall, Minerva McGonagall, Hermione Granger, Hermione Granger, Ron Weasley, Ron Weasley]], activities=[Learning, Teaching]]])
Activity(id=4, name=Learning, members=[Member [id=14, name=Hermione Granger, house=House [id=6, name=Gryffindor, members=15, memberName=[Albus Dumbledore, Harry Potter, Minerva McGonagall, Hermione Granger, Ron Weasley, Albus Dumbledore, Albus Dumbledore, Harry Potter, Harry Potter, Minerva McGonagall, Minerva McGonagall, Hermione Granger, Hermione Granger, Ron Weasley, Ron Weasley]], activities=[Learning, Teaching]]])
Activity(id=5, name=Unknown, members=[])

# all members
Member [id=10, name=Albus Dumbledore, house=House [id=6, name=Gryffindor, members=15, memberName=[Albus Dumbledore, Harry Potter, Minerva McGonagall, Hermione Granger, Ron Weasley, Albus Dumbledore, Albus Dumbledore, Harry Potter, Harry Potter, Minerva McGonagall, Minerva McGonagall, Hermione Granger, Hermione Granger, Ron Weasley, Ron Weasley]], activities=[]]
Member [id=11, name=Minerva McGonagall, house=House [id=6, name=Gryffindor, members=15, memberName=[Albus Dumbledore, Harry Potter, Minerva McGonagall, Hermione Granger, Ron Weasley, Albus Dumbledore, Albus Dumbledore, Harry Potter, Harry Potter, Minerva McGonagall, Minerva McGonagall, Hermione Granger, Hermione Granger, Ron Weasley, Ron Weasley]], activities=[]]
Member [id=12, name=Harry Potter, house=House [id=6, name=Gryffindor, members=15, memberName=[Albus Dumbledore, Harry Potter, Minerva McGonagall, Hermione Granger, Ron Weasley, Albus Dumbledore, Albus Dumbledore, Harry Potter, Harry Potter, Minerva McGonagall, Minerva McGonagall, Hermione Granger, Hermione Granger, Ron Weasley, Ron Weasley]], activities=[]]
Member [id=13, name=Ron Weasley, house=House [id=6, name=Gryffindor, members=15, memberName=[Albus Dumbledore, Harry Potter, Minerva McGonagall, Hermione Granger, Ron Weasley, Albus Dumbledore, Albus Dumbledore, Harry Potter, Harry Potter, Minerva McGonagall, Minerva McGonagall, Hermione Granger, Hermione Granger, Ron Weasley, Ron Weasley]], activities=[Eating, Playing]]
Member [id=14, name=Hermione Granger, house=House [id=6, name=Gryffindor, members=15, memberName=[Albus Dumbledore, Harry Potter, Minerva McGonagall, Hermione Granger, Ron Weasley, Albus Dumbledore, Albus Dumbledore, Harry Potter, Harry Potter, Minerva McGonagall, Minerva McGonagall, Hermione Granger, Hermione Granger, Ron Weasley, Ron Weasley]], activities=[Learning, Teaching]]
Member [id=15, name=Hengist of Woodcroft, house=House [id=7, name=Hufflepuff, members=3, memberName=[Hengist of Woodcroft, Newt Scamander, Artemisia Lufkin]], activities=[]]
Member [id=16, name=Newt Scamander, house=House [id=7, name=Hufflepuff, members=3, memberName=[Hengist of Woodcroft, Newt Scamander, Artemisia Lufkin]], activities=[]]
Member [id=17, name=Artemisia Lufkin, house=House [id=7, name=Hufflepuff, members=3, memberName=[Hengist of Woodcroft, Newt Scamander, Artemisia Lufkin]], activities=[]]
Member [id=18, name=Luna Lovegood, house=House [id=8, name=Ravenclaw, members=4, memberName=[Luna Lovegood, Gilderoy Lockheart, Ignatia Wildsmith, Garrick Ollivander]], activities=[]]
Member [id=19, name=Gilderoy Lockheart, house=House [id=8, name=Ravenclaw, members=4, memberName=[Luna Lovegood, Gilderoy Lockheart, Ignatia Wildsmith, Garrick Ollivander]], activities=[]]
Member [id=20, name=Ignatia Wildsmith, house=House [id=8, name=Ravenclaw, members=4, memberName=[Luna Lovegood, Gilderoy Lockheart, Ignatia Wildsmith, Garrick Ollivander]], activities=[]]
Member [id=21, name=Garrick Ollivander, house=House [id=8, name=Ravenclaw, members=4, memberName=[Luna Lovegood, Gilderoy Lockheart, Ignatia Wildsmith, Garrick Ollivander]], activities=[]]
Member [id=22, name=Tom Riddle, house=House [id=9, name=Slytherin, members=3, memberName=[Tom Riddle, Bellatrix Black, Draco Malfoy]], activities=[]]
Member [id=23, name=Bellatrix Black, house=House [id=9, name=Slytherin, members=3, memberName=[Tom Riddle, Bellatrix Black, Draco Malfoy]], activities=[]]
Member [id=24, name=Draco Malfoy, house=House [id=9, name=Slytherin, members=3, memberName=[Tom Riddle, Bellatrix Black, Draco Malfoy]], activities=[]]


```


##### HogwartsApplication.java

```java
package jpadata.relationship.bidirectional;

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.boot.CommandLineRunner;
import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;

@SpringBootApplication
public class HogwartsApplication implements CommandLineRunner {

  public static void main(String[] args) {
    SpringApplication.run(HogwartsApplication.class, args);
  }

  @Autowired
  private HogwartsHouse hogwartsHouse;

  @Override
  public void run(String... args) throws Exception {
    hogwartsHouse.houseAllocation();

  }

}
```


##### Member.java [Entity]

```java
package jpadata.relationship.bidirectional;

import java.util.ArrayList;
import java.util.List;
import java.util.stream.Collectors;
import javax.persistence.Entity;
import javax.persistence.GeneratedValue;
import javax.persistence.GenerationType;
import javax.persistence.Id;
import javax.persistence.JoinColumn;
import javax.persistence.JoinTable;
import javax.persistence.ManyToMany;
import javax.persistence.ManyToOne;
import javax.persistence.Table;
import javax.persistence.Transient;
import com.fasterxml.jackson.annotation.JsonIgnore;
import lombok.AllArgsConstructor;
import lombok.Data;
import lombok.NoArgsConstructor;

@Entity
@Data
@Table(name = "MEMBER")
@NoArgsConstructor
@AllArgsConstructor
public class Member {

  @Id
  @GeneratedValue(strategy = GenerationType.AUTO)
  private Integer id;

  private String name;

  @ManyToMany
  @JoinTable(name = "MEMBER_ACTIVITY", joinColumns = @JoinColumn(name = "MEMBER_ID", referencedColumnName = "ID"),
          inverseJoinColumns = @JoinColumn(name = "ACTIVITY_ID", referencedColumnName = "ID"))
  private List<Activity> activities = new ArrayList<>();

  @Transient
  public List<String> getActivityName() {
    return this.activities.stream().map(a -> a.getName()).collect(Collectors.toList());
  }

  public void addActivity(Activity... activities) {
    for (Activity activity : activities) {
      this.activities.add(activity);
      activity.addMember(this);
    }
  }

  @ManyToOne
  @JsonIgnore
  private House house;

  public void addHouse(House house) {
    this.house = house;
    house.addMember(this);
  }

  public Member(String name) {
    this.name = name;
  }

  @Override
  public String toString() {
    return "Member [id=" + id + ", name=" + name + ", house=" + house + ", activities=" + getActivityName() + "]";
  }

}

```


##### MemberRepository.java
```java
package jpadata.relationship.bidirectional;

import java.util.Optional;
import org.springframework.data.jpa.repository.JpaRepository;
import org.springframework.stereotype.Repository;

@Repository
public interface MemberRepository extends JpaRepository<Member, Integer> {

  Optional<Member> findByName(String name);
}

```


##### Activity.java [Entity]

```java
package jpadata.relationship.bidirectional;

import java.util.ArrayList;
import java.util.List;
import java.util.stream.Collectors;
import javax.persistence.Entity;
import javax.persistence.GeneratedValue;
import javax.persistence.GenerationType;
import javax.persistence.Id;
import javax.persistence.ManyToMany;
import javax.persistence.Table;
import javax.persistence.Transient;
import lombok.AllArgsConstructor;
import lombok.Data;
import lombok.NoArgsConstructor;

@Entity
@Data
@Table(name = "ACTIVITY")
@NoArgsConstructor
@AllArgsConstructor
public class Activity {

  @Id
  @GeneratedValue(strategy = GenerationType.AUTO)
  private Integer id;

  private String name;

  @ManyToMany(mappedBy = "activities")
  private List<Member> members = new ArrayList<>();

  @Transient
  public List<String> getMembersName() {
    return this.members.stream().map(m -> m.getName()).collect(Collectors.toList());
  }

  public void addMember(Member member) {
    this.members.add(member);
  }

  public Activity(String name) {
    this.name = name;
  }

}

```


##### ActivityRepository.java

```java
package jpadata.relationship.bidirectional;

import java.util.Optional;
import org.springframework.data.jpa.repository.JpaRepository;
import org.springframework.stereotype.Repository;

@Repository
public interface ActivityRepository extends JpaRepository<Activity, Integer> {
  
  Optional<Activity> findByName(String name);

}

```


##### House.java [Entity]

```java
package jpadata.relationship.bidirectional;

import java.util.ArrayList;
import java.util.List;
import java.util.stream.Collectors;
import javax.persistence.CascadeType;
import javax.persistence.Entity;
import javax.persistence.GeneratedValue;
import javax.persistence.GenerationType;
import javax.persistence.Id;
import javax.persistence.OneToMany;
import javax.persistence.Table;
import javax.persistence.Transient;
import lombok.AllArgsConstructor;
import lombok.Data;
import lombok.NoArgsConstructor;

@Entity
@Data
@Table(name = "HOUSE")
@NoArgsConstructor
@AllArgsConstructor
public class House {

  @Id
  @GeneratedValue(strategy = GenerationType.AUTO)
  private Integer id;

  private String name;

  @OneToMany(mappedBy = "house", cascade = CascadeType.ALL, orphanRemoval = true)
  private List<Member> members = new ArrayList<>();

  @Transient
  private List<String> memberName;

  public List<String> getMembersName() {
    memberName = members.stream().map(m -> m.getName()).collect(Collectors.toList());
    return memberName;
  }
  
  public void addMember(Member member) {
    this.members.add(member);
  }
  
  public void addMembers(Member...members) {
    for(Member member : members) {
      this.members.add(member);
      member.addHouse(this);
    }
  }

  public House(String name) {
    this.name = name;
  }

  @Override
  public String toString() {
    return "House [id=" + id + ", name=" + name + ", members=" + members.size() + ", memberName=" + getMembersName()
            + "]";
  }

}

```


##### HouseRepository.java

```java
package jpadata.relationship.bidirectional;

import java.util.Optional;
import org.springframework.data.jpa.repository.JpaRepository;
import org.springframework.stereotype.Repository;

@Repository
public interface HouseRepository extends JpaRepository<House, Integer> {
  
  Optional<House> findByName(String name);

}

```



##### HogwartsHouse.java [Service]

```java
package jpadata.relationship.bidirectional;

import java.util.Arrays;
import javax.transaction.Transactional;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Service;

@Service
public class HogwartsHouse {

  @Autowired
  private HouseRepository houseRepository;

  @Autowired
  private ActivityRepository activityRepository;

  @Autowired
  private MemberRepository memberRepository;

  public void hobby() {
    Activity eating = new Activity("Eating");
    Activity playing = new Activity("Playing");
    Activity teaching = new Activity("Teaching");
    Activity unknown = new Activity("Unknown");

    // activities are independent of member so we can create and persist them
    activityRepository.saveAll(Arrays.asList(eating, playing, teaching, unknown));
  }

  @Transactional
  public void houseAllocation() {
    // Many Activity To Many Member
    Activity eating = new Activity("Eating");
    Activity playing = new Activity("Playing");
    Activity teaching = new Activity("Teaching");
    Activity learning = new Activity("Learning");
    Activity unknown = new Activity("Unknown");

    // activities are independent of member so we can create and persist them
    activityRepository.saveAll(Arrays.asList(eating, playing, teaching, learning, unknown));

    // One House to Many Member
    House gryffindor = new House("Gryffindor");
    House hufflepuff = new House("Hufflepuff");
    House ravenclaw = new House("Ravenclaw");
    House slytherin = new House("Slytherin");

    // houses are independent of any student so we can create and save persist them independently
    houseRepository.saveAll(Arrays.asList(gryffindor, hufflepuff, ravenclaw, slytherin));

    // Gryffindor
    Member dumbledore = new Member("Albus Dumbledore");
    Member harry = new Member("Harry Potter");
    Member minerva = new Member("Minerva McGonagall");
    Member hermione = new Member("Hermione Granger");
    Member ron = new Member("Ron Weasley");

    ron.addActivity(eating, playing);
    hermione.addActivity(learning, teaching);

    dumbledore.addHouse(gryffindor);
    harry.addHouse(gryffindor);
    minerva.addHouse(gryffindor);
    hermione.addHouse(gryffindor);
    ron.addHouse(gryffindor);
    gryffindor.addMembers(dumbledore, harry, minerva, hermione, ron);

    // Hufflepuff
    Member hengist = new Member("Hengist of Woodcroft");
    Member scamander = new Member("Newt Scamander");
    Member lufkin = new Member("Artemisia Lufkin");

    hengist.addHouse(hufflepuff);
    scamander.addHouse(hufflepuff);
    lufkin.addHouse(hufflepuff);

    // Ravenclaw
    Member luna = new Member("Luna Lovegood");
    Member lockheart = new Member("Gilderoy Lockheart");
    Member wildshmith = new Member("Ignatia Wildsmith");
    Member olivander = new Member("Garrick Ollivander");

    luna.addHouse(ravenclaw);
    lockheart.addHouse(ravenclaw);
    wildshmith.addHouse(ravenclaw);
    olivander.addHouse(ravenclaw);

    // Slytherin
    Member tom = new Member("Tom Riddle");
    Member bellatrix = new Member("Bellatrix Black");
    Member draco = new Member("Draco Malfoy");

    tom.addHouse(slytherin);
    bellatrix.addHouse(slytherin);
    draco.addHouse(slytherin);

    // save members
    memberRepository.saveAll(Arrays.asList(dumbledore, minerva, harry, ron, hermione));
    memberRepository.saveAll(Arrays.asList(hengist, scamander, lufkin));
    memberRepository.saveAll(Arrays.asList(luna, lockheart, wildshmith, olivander));
    memberRepository.saveAll(Arrays.asList(tom, bellatrix, draco));

    // all houses
    System.out.println("all houses");
    houseRepository.findAll().stream().forEach(m -> System.out.println(m));

    // all activities
    System.out.println("all activities");
    activityRepository.findAll().stream().forEach(a -> System.out.println(a));

    // all members
    System.out.println("all members");
    memberRepository.findAll().stream().forEach(m -> System.out.println(m));

  }
}

```
