# Docker-Kubernetes
📅 [2020-05-01](https://arunsah.github.io/meta/changelog#2020-05-01) 🖊️ [@arunsah](https://github.com/arunsah) 🧭 [Pune, India](https://en.wikipedia.org/wiki/Hinjawadi)

---
### Installation

Get and install docker desktop (Docker v2.2.x ~700MB).


#### Test Installation

```
$ which docker
/usr/local/bin/docker

$ docker --version
Docker version 19.03.8, build afacb8b 

$ which kubectl
/usr/local/bin/kubectl

$ kubectl version
Client Version: version.Info{Major:"1", Minor:"17", GitVersion:"v1.17.3", GitCommit:"06ad960bfd03b39c8310aaf92d1e7c12ce618213", GitTreeState:"clean", BuildDate:"2020-02-11T18:14:22Z", GoVersion:"go1.13.6", Compiler:"gc", Platform:"darwin/amd64"}
Server Version: version.Info{Major:"1", Minor:"15", GitVersion:"v1.15.5", GitCommit:"20c265fef0741dd71a66480e35bd69f18351daea", GitTreeState:"clean", BuildDate:"2019-10-15T19:07:57Z", GoVersion:"go1.12.10", Compiler:"gc", Platform:"linux/amd64"}

```


### Creating Docker Image and Container
- Use image at https://hub.docker.com/r/tutum/hello-world/
- Valid ports is 30000-32767 to expose services on Kubernetes cluster for NodePort.


```
$ docker run -d -p 31313:80 tutum/hello-world

// now we can access the web service through curl or browser.
$ curl http://localhost:31313

// listing all images stored locally
$ docker images
REPOSITORY                           TAG                 IMAGE ID            CREATED             SIZE
tutum/hello-world                    latest              31e17b0746e4        4 years ago         17.8MB

// listing all containers
$ docker container ls
CONTAINER ID        IMAGE                                COMMAND                  CREATED             STATUS              PORTS                   NAMES
b97534c7e569        tutum/hello-world                    "/bin/sh -c 'php-fpm…"   17 minutes ago      Up 17 minutes       0.0.0.0:31313->80/tcp   heuristic_darwin

// stop running container with container-id
$ docker stop b97534c7e569
b97534c7e569

// remove/delete containers and images
$ docker system prune
WARNING! This will remove:
  - all stopped containers
  - all networks not used by at least one container
  - all dangling images
  - all dangling build cache

Are you sure you want to continue? [y/N]

// container information using container-name
$ docker inspect --format '{{ .NetworkSettings.IPAddress }}' heuristic_darwin
172.17.0.2

$ docker inspect heuristic_darwin


$ docker kill heuristic_darwin
heuristic_darwin

// running container with “rm” will remove the container once the container is stopped.
$ docker image rm tutum/hello-world
```

### Creating Kubernetes Deployment and Service

```
$ mkdir kuberneted-demo
$ cd kuberneted-demo/
$ nano k8.yml
$ ls
k8.yml

$ cat k8.yml 
apiVersion: apps/v1
kind: Deployment
metadata:
  name: greeting-service
  labels:
    app: greeting-service
spec:
  replicas: 3
  selector:
    matchLabels:
      app: greeting-service
  template:
    metadata:
      labels:
        app: greeting-service
    spec:
      containers: 
        - name: greeting-service-containers
          image: tutum/hello-world:latest
          # for local image
          # imagePullPolicy: Never
          env:
          - name: STATE
            value: local
          ports:
            - containerPort: 80
            
            
---

apiVersion: v1
kind: Service
metadata:
  name: greeting-service
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
    app: greeting-service
  type: NodePort
  


// create deployment and service
$ kubectl apply -f ./k8.yml 
deployment.apps/greeting-service created
service/greeting-service created

$ kubectl get deploy -o wide
NAME                          READY   UP-TO-DATE   AVAILABLE   AGE   CONTAINERS                               IMAGES                     SELECTOR
greeting-service   3/3     3            3           22s   greeting-service-containers   tutum/hello-world:latest   app=greeting-service 

$ kubectl get pods -o wide
NAME                                           READY   STATUS    RESTARTS   AGE   IP          NODE             NOMINATED NODE   READINESS GATES
greeting-service-5dbcb58ff5-jk457   1/1     Running   0          56s   10.1.0.98   docker-desktop   <none>           <none>
greeting-service-5dbcb58ff5-tsncl   1/1     Running   0          56s   10.1.0.96   docker-desktop   <none>           <none>
greeting-service-5dbcb58ff5-x9g27   1/1     Running   0          56s   10.1.0.97   docker-desktop   <none>           <none>

$ kubectl get service -o wide
NAME                          TYPE        CLUSTER-IP      EXTERNAL-IP   PORT(S)          AGE   SELECTOR
greeting-service   NodePort    10.110.150.15   <none>        9090:31313/TCP   83s   app=greeting-service
kubernetes                    ClusterIP   10.96.0.1       <none>        443/TCP          11d   <none>

$ curl http://localhost:31313

// run below command and observe the hostname in the output.
// the hostname will keep changing since the request is processed by different application instance.
$ while true; do curl http://localhost:31313; sleep 1; done;


//NOTE: Killing individual PODS will not kill the it as 
// Kubernetes will make sure to required number pods as per specification.

// delete deployment and service
$ kubectl delete deployment greeting-service
deployment.extensions "greeting-service" deleted

$ kubectl delete service greeting-service
service "greeting-service" deleted

```

### Common Commands

```
$ curl --location --request GET 'http://localhost:9090/greeting-service/hello' --header 'username: mario'
$ docker kill greeting-service-container-sts
$ docker stop f186e6f90157
$ docker stats --format "table {{.Container}}\t {{.CPUPerc}}\t{{.MemUsage}}\t {{.Name}}"

$ kubectl get deploy -o wide
$ kubectl get pods -o wide
$ kubectl get service -o wide
$ docker image rm greeting-service-image:v1
// $ cd <project root directory>
$ kubectl delete deployment oal-epmdrm-service
$ kubectl delete service oal-epmdrm-service

$ docker build -t greeting-service-image:v1 .
$ kubectl apply -f ./src/main/resources/k8/k8.yml
$ kubectl apply -f ./src/main/resources/k8/deployment.yml
$ kubectl apply -f ./src/main/resources/k8/service.yaml

$ while true; do curl --location --request GET 'http://localhost:30002/greeting-service/hello' --header 'username: mario'; sleep 1; done;
$ curl --location --request GET 'http://localhost:30002/greeting-service/actuator' --header 'username: mario' -d'username=user&password=admin'
$ ab -H 'username: mario' -n 100 -c 10 'http://localhost:30002/greeting-service/hello'
```

### Memory Usage on Kubernetes Cluster

```
$ kubectl describe nodes
Name:               docker-desktop
Roles:              master
Labels:             beta.kubernetes.io/arch=amd64
                    beta.kubernetes.io/os=linux
                    kubernetes.io/arch=amd64
                    kubernetes.io/hostname=docker-desktop
                    kubernetes.io/os=linux
                    node-role.kubernetes.io/master=
Annotations:        kubeadm.alpha.kubernetes.io/cri-socket: /var/run/dockershim.sock
                    node.alpha.kubernetes.io/ttl: 0
                    volumes.kubernetes.io/controller-managed-attach-detach: true
CreationTimestamp:  Tue, 05 May 2020 13:33:24 +0530
Taints:             <none>
Unschedulable:      false
Lease:
  HolderIdentity:  docker-desktop
  AcquireTime:     <unset>
  RenewTime:       Tue, 05 May 2020 21:21:02 +0530
Conditions:
  Type             Status  LastHeartbeatTime                 LastTransitionTime                Reason                       Message
  ----             ------  -----------------                 ------------------                ------                       -------
  MemoryPressure   False   Tue, 05 May 2020 21:20:37 +0530   Tue, 05 May 2020 13:33:20 +0530   KubeletHasSufficientMemory   kubelet has sufficient memory available
  DiskPressure     False   Tue, 05 May 2020 21:20:37 +0530   Tue, 05 May 2020 13:33:20 +0530   KubeletHasNoDiskPressure     kubelet has no disk pressure
  PIDPressure      False   Tue, 05 May 2020 21:20:37 +0530   Tue, 05 May 2020 13:33:20 +0530   KubeletHasSufficientPID      kubelet has sufficient PID available
  Ready            True    Tue, 05 May 2020 21:20:37 +0530   Tue, 05 May 2020 13:33:20 +0530   KubeletReady                 kubelet is posting ready status
Addresses:
  InternalIP:  192.168.65.3
  Hostname:    docker-desktop
Capacity:
  cpu:                5
  ephemeral-storage:  61255492Ki
  hugepages-1Gi:      0
  hugepages-2Mi:      0
  memory:             12271740Ki
  pods:               110
Allocatable:
  cpu:                5
  ephemeral-storage:  56453061334
  hugepages-1Gi:      0
  hugepages-2Mi:      0
  memory:             12169340Ki
  pods:               110
System Info:
  Machine ID:                 8c5e387a-bfc2-43b6-b2c1-76e46c1c8ec9
  System UUID:                2e2c4a86-0000-0000-ba0b-b54adcbbbce9
  Boot ID:                    3587f277-045e-4efd-9586-81c9dab556f6
  Kernel Version:             4.19.76-linuxkit
  OS Image:                   Docker Desktop
  Operating System:           linux
  Architecture:               amd64
  Container Runtime Version:  docker://19.3.8
  Kubelet Version:            v1.15.5
  Kube-Proxy Version:         v1.15.5
Non-terminated Pods:          (24 in total)
  Namespace                   Name                                      CPU Requests  CPU Limits    Memory Requests  Memory Limits     AGE
  ---------                   ----                                      ------------  ----------    ---------------  -------------     ---
  default                     myapp-v1-796dd8845c-xzcsh                 0 (0%)        0 (0%)        0 (0%)           0 (0%)            6h25m
  default                     myapp-v2-ff68b5b69-nkfr2                  0 (0%)        0 (0%)        0 (0%)           0 (0%)            6h25m
  docker                      compose-7b7c5cbbcc-ttwkz                  0 (0%)        0 (0%)        0 (0%)           0 (0%)            7h46m
  docker                      compose-api-dbbf7c5db-5r4sh               0 (0%)        0 (0%)        0 (0%)           0 (0%)            7h46m
  istio-system                grafana-584949b9c6-rs25v                  10m (0%)      0 (0%)        0 (0%)           0 (0%)            6h50m
  istio-system                istio-citadel-7998dbbd9c-x4kmd            10m (0%)      0 (0%)        0 (0%)           0 (0%)            6h50m
  istio-system                istio-egressgateway-769fd9869f-vrk4z      10m (0%)      2 (40%)       40Mi (0%)        1Gi (8%)          6h50m
  istio-system                istio-galley-5cb68c8bdb-tsk6h             10m (0%)      0 (0%)        0 (0%)           0 (0%)            6h50m
  istio-system                istio-ingressgateway-67c9b549cb-8p2r8     10m (0%)      2 (40%)       40Mi (0%)        1Gi (8%)          6h50m
  istio-system                istio-pilot-6d84c7c7d7-kxf5d              20m (0%)      2 (40%)       140Mi (1%)       1Gi (8%)          6h50m
  istio-system                istio-policy-bd4db6dff-2x2kl              20m (0%)      2 (40%)       140Mi (1%)       1Gi (8%)          6h50m
  istio-system                istio-sidecar-injector-69c57976b-xcz7h    10m (0%)      0 (0%)        0 (0%)           0 (0%)            6h50m
  istio-system                istio-telemetry-57fb5464f4-ljr47          60m (1%)      6800m (136%)  140Mi (1%)       5073741824 (40%)  6h50m
  istio-system                istio-tracing-68ffb9d456-dnzpq            10m (0%)      0 (0%)        0 (0%)           0 (0%)            6h50m
  istio-system                kiali-7d4cf866cc-9dllr                    10m (0%)      0 (0%)        0 (0%)           0 (0%)            6h50m
  istio-system                prometheus-8685f659f-m6gjl                10m (0%)      0 (0%)        0 (0%)           0 (0%)            6h50m
  kube-system                 coredns-5c98db65d4-r4zkh                  100m (2%)     0 (0%)        70Mi (0%)        170Mi (1%)        7h47m
  kube-system                 coredns-5c98db65d4-tssln                  100m (2%)     0 (0%)        70Mi (0%)        170Mi (1%)        7h47m
  kube-system                 etcd-docker-desktop                       0 (0%)        0 (0%)        0 (0%)           0 (0%)            7h46m
  kube-system                 kube-apiserver-docker-desktop             250m (5%)     0 (0%)        0 (0%)           0 (0%)            7h46m
  kube-system                 kube-controller-manager-docker-desktop    200m (4%)     0 (0%)        0 (0%)           0 (0%)            7h46m
  kube-system                 kube-proxy-tlcxp                          0 (0%)        0 (0%)        0 (0%)           0 (0%)            7h47m
  kube-system                 kube-scheduler-docker-desktop             100m (2%)     0 (0%)        0 (0%)           0 (0%)            7h46m
  kube-system                 storage-provisioner                       0 (0%)        0 (0%)        0 (0%)           0 (0%)            7h46m
Allocated resources:
  (Total limits may be over 100 percent, i.e., overcommitted.)
  Resource           Requests    Limits
  --------           --------    ------
  cpu                940m (18%)  14800m (296%)
  memory             640Mi (5%)  9497290Ki (78%)
  ephemeral-storage  0 (0%)      0 (0%)
Events:              <none>

```

### Minukube

```
Minikube Commands:
Last login: Tue Mar 31 19:32:20 on ttys002
$ minikube status
host: Stopped
kubelet: Stopped
apiserver: Stopped
kubeconfig: Stopped

$ minikube delete
🔥  Deleting "minikube" in virtualbox ...
💀  Removed all traces of the "minikube" cluster.

$ minikube start
😄  minikube v1.7.3 on Darwin 10.14.6
✨  Automatically selected the hyperkit driver. Other choices: virtualbox, docker (experimental)
💾  Downloading driver docker-machine-driver-hyperkit:
    > docker-machine-driver-hyperkit.sha256: 65 B / 65 B [---] 100.00% ? p/s 0s
    > docker-machine-driver-hyperkit: 10.88 MiB / 10.88 MiB  100.00% 284.09 KiB
🔑  The 'hyperkit' driver requires elevated permissions. The following commands will be executed:

    $ sudo chown root:wheel /Users/arunsah/.minikube/bin/docker-machine-driver-hyperkit 
    $ sudo chmod u+s /Users/arunsah/.minikube/bin/docker-machine-driver-hyperkit 


Password:
🔥  Creating hyperkit VM (CPUs=2, Memory=2000MB, Disk=20000MB) ...
⚠️  Node may be unable to resolve external DNS records
⚠️  VM is unable to access k8s.gcr.io, you may need to configure a proxy or set --image-repository
🐳  Preparing Kubernetes v1.17.3 on Docker 19.03.6 ...
🚀  Launching Kubernetes ... 
🌟  Enabling addons: default-storageclass, storage-provisioner
⌛  Waiting for cluster to come online ...
🏄  Done! kubectl is now configured to use "minikube"
$ minikube start
😄  minikube v1.7.3 on Darwin 10.14.6
✨  Using the hyperkit driver based on existing profile
⌛  Reconfiguring existing host ...
🏃  Using the running hyperkit "minikube" VM ...
⚠️  Node may be unable to resolve external DNS records
⚠️  VM is unable to access k8s.gcr.io, you may need to configure a proxy or set --image-repository
🐳  Preparing Kubernetes v1.17.3 on Docker 19.03.6 ...
🚀  Launching Kubernetes ... 
🌟  Enabling addons: default-storageclass, storage-provisioner
🏄  Done! kubectl is now configured to use "minikube"

$ minikube status
host: Running
kubelet: Running
apiserver: Running
kubeconfig: Configured

$ eval $(minikube docker-env)
$ minikube docker-env
export DOCKER_TLS_VERIFY="1"
export DOCKER_HOST="tcp://192.168.99.104:2376"
export DOCKER_CERT_PATH="/Users/arunsah/.minikube/certs"
export MINIKUBE_ACTIVE_DOCKERD="minikube"
# To point your shell to minikube's docker-daemon, run:
# eval $(minikube -p minikube docker-env)


$ minikube stop
✋  Stopping "minikube" in hyperkit ...
🛑  "minikube" stopped.

```

### Alpine Linux Package Manager
- [https://wiki.alpinelinux.org/wiki/How_to_get_regular_stuff_working](https://wiki.alpinelinux.org/wiki/How_to_get_regular_stuff_working) 

```
apk add curl
apk add curl-doc
```


### References
- https://kubernetes.io/docs/home/
- https://docs.docker.com/
- [Dockerfile reference - Docker Documentation](https://docs.docker.com/engine/reference/builder/)
- https://stackoverflow.com/questions/55462654/cant-access-minikube-loadbalancer-service-from-host-machine
- https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.10/#service-v1-core
- https://hub.docker.com/r/tutum/hello-world/
- [https://hub.docker.com/editions/community/docker-ce-desktop-windows](https://hub.docker.com/editions/community/docker-ce-desktop-windows)
- [https://hub.docker.com/editions/community/docker-ce-desktop-mac/](https://hub.docker.com/editions/community/docker-ce-desktop-mac/) 
- Benchmarking:
	- https://docs.docker.com/engine/reference/commandline/stats/
	- https://sysdig.com/blog/kubernetes-monitoring-prometheus/
