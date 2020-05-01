# Spinnaker on Kubernetes	
#spinnaker #kubernetes #deployment #may2020 

---
- [Spinnaker](https://www.spinnaker.io/)  as the multicloud deployment tool.
- [Helm](https://github.com/kubernetes/helm) makes installing applications in Kubernetes extremely easy. Each application is packaged as a Chart, a deployable unit of Helm. Setup Helm before installing Spinnaker Chart.


### Installing Helm

```

$ brew install wget
$ wget https://storage.googleapis.com/kubernetes-helm/helm-v2.13.0-darwin-amd64.tar.gz
$ tar -zxvf helm-v2.13.0-darwin-amd64.tar.gz
$ chmod +x ./darwin-amd64/helm
$ mv ./darwin-amd64/helm /usr/local/bin/

// We will now install Helm and verify it
$ helm init
Creating /Users/arunsah/.helm 
Creating /Users/arunsah/.helm/repository 
Creating /Users/arunsah/.helm/repository/cache 
Creating /Users/arunsah/.helm/repository/local 
Creating /Users/arunsah/.helm/plugins 
Creating /Users/arunsah/.helm/starters 
Creating /Users/arunsah/.helm/cache/archive 
Creating /Users/arunsah/.helm/repository/repositories.yaml 
Adding stable repo with URL: https://kubernetes-charts.storage.googleapis.com 
Adding local repo with URL: http://127.0.0.1:8879/charts 
$HELM_HOME has been configured at /Users/arunsah/.helm.

Tiller (the Helm server-side component) has been installed into your Kubernetes Cluster.
Happy Helming!

$ helm version
Client: &version.Version{SemVer:"v2.13.0", GitCommit:"8478fb4fc723885b155c924d1c8c410b7a9444e6", GitTreeState:"clean"}
Server: &version.Version{SemVer:"v2.13.0", GitCommit:"8478fb4fc723885b155c924d1c8c410b7a9444e6", GitTreeState:"clean"}

// The above output confirms that Helm and Tiller, 
// the server-side component of Helm are properly installed. 
// Tiller runs as a Kubernetes Pod and Service within the kube-system namespace.


// When you want to upgrade Tiller, just run helm init --upgrade
$ helm init --upgrade
```


### Installing Spinnaker through Helm Chart

```
// Before we deploy Spinnaker, we need a configuration file in YAML format, 
// which will provide the initial set of configuration values. 
// Grab this file from the Github Spinnaker Helm Chart repository.

$ curl -Lo values.yaml https://raw.githubusercontent.com/kubernetes/charts/master/stable/spinnaker/values.yaml

// installing Spinnaker
$ helm install -n kubelive stable/spinnaker -f values.yaml --timeout 300  --version 0.3.5 --namespace spinnaker


$ helm install -n kubelive stable/spinnaker -f values.yaml --timeout 300  --namespace spinnaker
Error: a release named kubelive already exists.
Run: helm ls --all kubelive; to check the status of the release
Or run: helm del --purge kubelive; to delete it


$ helm del --purge kubelive
^C
$ helm reset
Tiller (the Helm server-side component) has been uninstalled from your Kubernetes Cluster.
$ helm init
$HELM_HOME has been configured at /Users/arunsah/.helm.

Tiller (the Helm server-side component) has been installed into your Kubernetes Cluster.

Please note: by default, Tiller is deployed with an insecure 'allow unauthenticated users' policy.
To prevent this, run `helm init` with the --tiller-tls-verify flag.
For more information on securing your installation see: https://docs.helm.sh/using_helm/#securing-your-helm-installation
Happy Helming!
$ helm install -n kubelive stable/spinnaker -f values.yaml --timeout 300  --namespace spinnaker


h$ helm ls --all kubelive
NAME    	REVISION	UPDATED                 	STATUS	CHART          	APP VERSION	NAMESPACE
kubelive	1       	Tue Apr 28 13:15:40 2020	FAILED	spinnaker-0.3.5	1.1.0      	spinnaker
$ 


$ helm install -n kubelive2 stable/spinnaker -f values.yaml --timeout 300  --namespace spinnaker
Error: timed out waiting for the condition
$ helm ls --all
NAME     	REVISION	UPDATED                 	STATUS	CHART           	APP VERSION	NAMESPACE
kubelive 	1       	Tue Apr 28 13:15:40 2020	FAILED	spinnaker-0.3.5 	1.1.0      	spinnaker
kubelive2	1       	Tue Apr 28 13:23:39 2020	FAILED	spinnaker-1.23.3	1.16.2     	spinnaker

```

### Issue: Timeout error
- I experienced the same problem on my test cluster but resolved it by increasing the node size. Error: timed out waiting for the condition (what condition) seems like a bug though. spinnaker docs say 8gb of ram in your nodes so… yeah. - [Spinnaker chart installation times out · Issue #2510 · helm/charts · GitHub](https://github.com/helm/charts/issues/2510)


```
$ helm install -n kubelive stable/spinnaker -f values.yaml  --namespace spinnaker
NAME:   kubelive
LAST DEPLOYED: Tue Apr 28 14:00:11 2020
NAMESPACE: spinnaker
STATUS: DEPLOYED

RESOURCES:
==> v1/ClusterRoleBinding
NAME                          AGE
kubelive-spinnaker-spinnaker  3m12s

==> v1/ConfigMap
NAME                                               DATA  AGE
kubelive-minio                                     2     3m12s
kubelive-spinnaker-additional-profile-config-maps  2     3m12s
kubelive-spinnaker-halyard-config                  3     3m12s
kubelive-spinnaker-halyard-init-script             1     3m12s
kubelive-spinnaker-service-settings                2     3m12s

==> v1/PersistentVolumeClaim
NAME            STATUS  VOLUME                                    CAPACITY  ACCESS MODES  STORAGECLASS  AGE
kubelive-minio  Bound   pvc-aca278bf-b430-4d9f-9d54-8ed5a2efc1b4  10Gi      RWO           hostpath      3m12s

==> v1/Pod(related)
NAME                             READY  STATUS   RESTARTS  AGE
kubelive-minio-64669d9cf8-qmqgh  1/1    Running  0         3m11s
kubelive-redis-master-0          1/1    Running  0         3m11s
kubelive-spinnaker-halyard-0     1/1    Running  0         3m11s

==> v1/RoleBinding
NAME                        AGE
kubelive-spinnaker-halyard  3m12s

==> v1/Secret
NAME                         TYPE    DATA  AGE
kubelive-minio               Opaque  2     3m12s
kubelive-redis               Opaque  1     3m12s
kubelive-spinnaker-registry  Opaque  1     3m12s

==> v1/Service
NAME                        TYPE       CLUSTER-IP     EXTERNAL-IP  PORT(S)   AGE
kubelive-minio              ClusterIP  None           <none>       9000/TCP  3m12s
kubelive-redis-master       ClusterIP  10.101.142.61  <none>       6379/TCP  3m12s
kubelive-spinnaker-halyard  ClusterIP  None           <none>       8064/TCP  3m11s

==> v1/ServiceAccount
NAME                        SECRETS  AGE
kubelive-spinnaker-halyard  1        3m12s

==> v1/StatefulSet
NAME                        READY  AGE
kubelive-spinnaker-halyard  1/1    3m11s

==> v1beta2/Deployment
NAME            READY  UP-TO-DATE  AVAILABLE  AGE
kubelive-minio  1/1    1           1          3m11s

==> v1beta2/StatefulSet
NAME                   READY  AGE
kubelive-redis-master  1/1    3m11s


NOTES:
1. You will need to create 2 port forwarding tunnels in order to access the Spinnaker UI:
  export DECK_POD=$(kubectl get pods --namespace spinnaker -l "cluster=spin-deck" -o jsonpath="{.items[0].metadata.name}")
  kubectl port-forward --namespace spinnaker $DECK_POD 9000

  export GATE_POD=$(kubectl get pods --namespace spinnaker -l "cluster=spin-gate" -o jsonpath="{.items[0].metadata.name}")
  kubectl port-forward --namespace spinnaker $GATE_POD 8084

2. Visit the Spinnaker UI by opening your browser to: http://127.0.0.1:9000

To customize your Spinnaker installation. Create a shell in your Halyard pod:

  kubectl exec --namespace spinnaker -it kubelive-spinnaker-halyard-0 bash

For more info on using Halyard to customize your installation, visit:
  https://www.spinnaker.io/reference/halyard/

For more info on the Kubernetes integration for Spinnaker, visit:
  https://www.spinnaker.io/reference/providers/kubernetes-v2/

$ 


$ kubectl get pod --namespace=spinnaker
NAME                                READY   STATUS      RESTARTS   AGE
kubelive-install-using-hal-wqsbw    0/1     Completed   0          5m6s
kubelive-minio-64669d9cf8-qmqgh     1/1     Running     0          5m6s
kubelive-redis-master-0             1/1     Running     0          5m6s
kubelive-spinnaker-halyard-0        1/1     Running     0          5m6s
spin-clouddriver-84999f6678-pjsr5   1/1     Running     0          2m18s
spin-deck-7f4b56c947-th7hv          1/1     Running     0          2m17s
spin-echo-55d95c59fc-zdlr5          1/1     Running     0          2m18s
spin-front50-6847ff9976-n8627       1/1     Running     0          2m11s
spin-gate-6d8c456d85-wlrlh          1/1     Running     0          2m15s
spin-igor-85d697bb79-f4gp8          0/1     Running     0          2m17s
spin-orca-9cf694bb8-d6pxq           1/1     Running     0          2m16s
spin-rosco-9b84d49cb-j5q75          1/1     Running     0          2m10s
$ 
```

Before we access the Spinnaker dashboard from the browser, we need to enable port forwarding by running the below commands. This exposes the Pod that runs the Spinnaker web UI to the host.

```
NOTES:
1. You will need to create 2 port forwarding tunnels in order to access the Spinnaker UI:
  $ export DECK_POD=$(kubectl get pods --namespace spinnaker -l "cluster=spin-deck" -o jsonpath="{.items[0].metadata.name}")
  $ kubectl port-forward --namespace spinnaker $DECK_POD 9000

  $ export GATE_POD=$(kubectl get pods --namespace spinnaker -l "cluster=spin-gate" -o jsonpath="{.items[0].metadata.name}")
  $ kubectl port-forward --namespace spinnaker $GATE_POD 8084

2. Visit the Spinnaker UI by opening your browser to: http://127.0.0.1:9000

To customize your Spinnaker installation. Create a shell in your Halyard pod:

  kubectl exec --namespace spinnaker -it kubelive-spinnaker-halyard-0 bash

For more info on using Halyard to customize your installation, visit:
  https://www.spinnaker.io/reference/halyard/

For more info on the Kubernetes integration for Spinnaker, visit:
  https://www.spinnaker.io/reference/providers/kubernetes-v2/

```

## kubernetes port forwarding

```
$ kubectl create namespace ns2
$ kubectl create -f port_fw2.yaml  # [1]
$ kubectl port-forward -n ns2 pod/pfpod 9992:80 &
nc 127.0.0.1 9992  # this will output a number of x characters, and will hang.
$ kubectl logs -n ns2 pf/pod -c portforwardtester

```


### Issue: Freezing of port forwarding

- The behaviour you see is expected. This command does not get daemonized by default. It will be forwarding the port until you kill the command with CTRL-C or other similar methods. You could try using & at the end of the command if you want to continue using that prompt. Personally I would use a terminal multiplexer like tmux or screen. - https://stackoverflow.com/a/48866118


```
$ export DECK_POD=$(kubectl get pods —namespace spinnaker -l “cluster=spin-deck” -o jsonpath=“{.items[0].metadata.name}”)
$ echo $DECK_POD
spin-deck-7f4b56c947-th7hv
$ kubectl port-forward —namespace spinnaker $DECK_POD 9000
Unable to listen on port 9000: Listeners failed to create with the following errors: [unable to create listener: Error listen tcp4 127.0.0.1:9000: bind: address already in use unable to create listener: Error listen tcp6 [::1]:9000: bind: address already in use]
error: unable to listen on any of the requested ports: [{9000 9000}]


$ export GATE_POD=$(kubectl get pods --namespace spinnaker -l "cluster=spin-gate" -o jsonpath="{.items[0].metadata.name}")
$ echo $GATE_POD
spin-gate-6d8c456d85-wlrlh
$ kubectl port-forward --namespace spinnaker $GATE_POD 8084 &
[1] 60447
$ Forwarding from 127.0.0.1:8084 -> 8084
Forwarding from [::1]:8084 -> 8084
```

### Creating Application
- Start by creating an application by clicking on Create Application under the Actions menu on the right top corner. 
- An “application” here is a logical collection of various resources such as Load Balancers, Security Groups, Server Groups, and Clusters.


```
apiVersion: apps/v1 # for versions before 1.9.0 use apps/v1beta2
kind: Deployment
metadata:
  name: nginx-deployment
spec:
  selector:
    matchLabels:
      app: nginx
  replicas: 2 # tells deployment to run 2 pods matching the template
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
      - name: nginx
        image: nginx:1.14.2
        ports:
        - containerPort: 80
```

```
apiVersion: v1
kind: Service
metadata:
  name: nginx-service
spec:
  ports:
      - protocol: "TCP"
        # Port accessible inside cluster
        port: 9090
        # Port to forward to inside the pod
        targetPort: 80
        # Port accessible outside cluster
        nodePort: 31313
  selector:
    app: nginx
  type: NodePort

```

### Resetting Helm

```
$ helm reset
Error: there are still 1 deployed releases (Tip: use —force to remove Tiller. Releases will not be deleted.)
$ helm delete keepalive
Error: release: “keepalive” not found
$ helm reset —force
Tiller (the Helm server-side component) has been uninstalled from your Kubernetes Cluster.
$ helm list
Error: could not find a ready tiller pod
```

### Resources
- https://thenewstack.io/getting-started-spinnaker-kubernetes/
- [Spinnaker](https://www.spinnaker.io/)  as the multicloud deployment tool.
- [Helm](https://github.com/kubernetes/helm) 
- [Helm - Using Helm](https://helm.sh/docs/intro/using_helm/)
- [Helm - Migrating Helm v2 to v3](https://helm.sh/docs/topics/v2_v3_migration/)
