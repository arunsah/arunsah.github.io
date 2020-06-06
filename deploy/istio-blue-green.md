# Blue Green Deployment with Kubernetes and Istio
📅 [2020-06-06](https://arunsah.github.io/meta/changelog#2020-06-06) 🖊️ [@arunsah](https://github.com/arunsah) 🧭 [Pune, India](https://en.wikipedia.org/wiki/Hinjawadi)

---


- We need at least 8GB of RAM and 4 core CPU to run Istio on Minikube. 

### Install Istio

```
$ curl -L https://git.io/getLatestIstio | sh -

$ chmod +x ./istio-1.5.2/bin
$ mv ./istio-1.5.2 /usr/local/bin/

$ 	
$ cat ~/.bash_profile 
export PATH=“/Users/arunsah/bin/kafka_2.13-2.4.0/bin:$PATH”

marioc:bin arunsah$ nano ~/.bash_profile
marioc:bin arunsah$ cat ~/.bash_profile 
export PATH="/Users/arunsah/bin/istio/istio-1.5.2:/Users/arunsah/bin/istio/istio-1.5.2/bin:/Users/arunsah/bin/Postman.app:/Users/arunsah/bin/kafka_2.13-2.4.0/bin:$PATH"


marioc:istio-1.5.2 arunsah$ cd bin/
marioc:bin arunsah$ ls
istioctl
```

```
marioc:spinnaker arunsah$ curl -L https://git.io/getLatestIstio | sh -
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
  0     0    0     0    0     0      0      0 —:—:—  0:01:16 —:—:—     0
100  3896  100  3896    0     0     50      0  0:01:17  0:01:17 —:—:—    50
Downloading istio-1.5.2 from https://github.com/istio/istio/releases/download/1.5.2/istio-1.5.2-osx.tar.gz …
Istio 1.5.2 Download Complete!

Istio has been successfully downloaded into the istio-1.5.2 folder on your system.

Next Steps:
See https://istio.io/docs/setup/kubernetes/install/ to add Istio to your Kubernetes cluster.

To configure the istioctl client tool for your workstation,
add the /Users/arunsah/dev/tut/spinnaker/istio-1.5.2/bin directory to your environment path variable with:
	 export PATH=“$PATH:/Users/arunsah/dev/tut/spinnaker/istio-1.5.2/bin”

Begin the Istio pre-installation verification check by running:
	 istioctl verify-install 

Need more information? Visit https://istio.io/docs/setup/kubernetes/install/ 
marioc:spinnaker arunsah$ ls
darwin-amd64				helm-v2.7.2-darwin-amd64.tar.gz		values.yaml
helm-v2.13.0-darwin-amd64.tar.gz	istio-1.5.2
```


```
marioc:istio-1.5.2 arunsah$ pwd
/Users/arunsah/bin/istio/istio-1.5.2

$ cd /Users/arunsah/bin/istio/istio-1.5.2
```

### Verify Installation

[Running Visual Studio Code on macOS](https://code.visualstudio.com/docs/setup/mac#_launching-from-the-command-line)

```
marioc:bin arunsah$ istioctl verify-install 

Checking the cluster to make sure it is ready for Istio installation...

#1. Kubernetes-api
-----------------------
Can initialize the Kubernetes client.
Can query the Kubernetes API Server.

#2. Kubernetes-version
-----------------------
Istio is compatible with Kubernetes: v1.15.5.

#3. Istio-existence
-----------------------
Istio will be installed in the istio-system namespace.

#4. Kubernetes-setup
-----------------------
Can create necessary Kubernetes configurations: Namespace,ClusterRole,ClusterRoleBinding,CustomResourceDefinition,Role,ServiceAccount,Service,Deployments,ConfigMap. 

#5. SideCar-Injector
-----------------------
This Kubernetes cluster supports automatic sidecar injection. To enable automatic sidecar injection see https://istio.io/docs/setup/kubernetes/additional-setup/sidecar-injection/#deploying-an-app

-----------------------
Install Pre-Check passed! The cluster is ready for Istio installation.


$ code ./install/kubernetes/istio-demo.yaml 
```



```
apiVersion: v1
kind: Service
metadata:
  name: istio-ingressgateway
  namespace: istio-system
  annotations:
  labels:
    chart: gateways
    heritage: Tiller
    release: istio
    app: istio-ingressgateway
    istio: ingressgateway
spec:
  type: LoadBalancer # change this to NodePort
  selector:
    release: istio
    app: istio-ingressgateway
    istio: ingressgateway
```


- Note these file is not available in new version. Check below link`$ kubectl apply -f install/kubernetes/helm/istio/templates/crds.yaml `
https://github.com/istio/istio.io/issues/3176
```
marioc:istio-1.5.2 arunsah$ kubectl apply -f ./install/kubernetes/helm/istio-init/files
customresourcedefinition.apiextensions.k8s.io/meshpolicies.authentication.istio.io created
customresourcedefinition.apiextensions.k8s.io/policies.authentication.istio.io created
customresourcedefinition.apiextensions.k8s.io/httpapispecs.config.istio.io created
customresourcedefinition.apiextensions.k8s.io/httpapispecbindings.config.istio.io created
customresourcedefinition.apiextensions.k8s.io/quotaspecs.config.istio.io created
customresourcedefinition.apiextensions.k8s.io/quotaspecbindings.config.istio.io created
customresourcedefinition.apiextensions.k8s.io/destinationrules.networking.istio.io created
customresourcedefinition.apiextensions.k8s.io/envoyfilters.networking.istio.io created
customresourcedefinition.apiextensions.k8s.io/gateways.networking.istio.io created
customresourcedefinition.apiextensions.k8s.io/serviceentries.networking.istio.io created
customresourcedefinition.apiextensions.k8s.io/sidecars.networking.istio.io created
customresourcedefinition.apiextensions.k8s.io/virtualservices.networking.istio.io created
customresourcedefinition.apiextensions.k8s.io/attributemanifests.config.istio.io created
customresourcedefinition.apiextensions.k8s.io/handlers.config.istio.io created
customresourcedefinition.apiextensions.k8s.io/instances.config.istio.io created
customresourcedefinition.apiextensions.k8s.io/rules.config.istio.io created
customresourcedefinition.apiextensions.k8s.io/clusterrbacconfigs.rbac.istio.io created
customresourcedefinition.apiextensions.k8s.io/rbacconfigs.rbac.istio.io created
customresourcedefinition.apiextensions.k8s.io/serviceroles.rbac.istio.io created
customresourcedefinition.apiextensions.k8s.io/servicerolebindings.rbac.istio.io created
customresourcedefinition.apiextensions.k8s.io/authorizationpolicies.security.istio.io created
customresourcedefinition.apiextensions.k8s.io/peerauthentications.security.istio.io created
customresourcedefinition.apiextensions.k8s.io/requestauthentications.security.istio.io created
customresourcedefinition.apiextensions.k8s.io/clusterissuers.certmanager.k8s.io created
customresourcedefinition.apiextensions.k8s.io/issuers.certmanager.k8s.io created
customresourcedefinition.apiextensions.k8s.io/certificates.certmanager.k8s.io created
customresourcedefinition.apiextensions.k8s.io/orders.certmanager.k8s.io created
customresourcedefinition.apiextensions.k8s.io/challenges.certmanager.k8s.io created
customresourcedefinition.apiextensions.k8s.io/adapters.config.istio.io created
customresourcedefinition.apiextensions.k8s.io/templates.config.istio.io created
marioc:istio-1.5.2 arunsah$ 
```


`$ kubectl apply -f install/kubernetes/istio-demo.yaml`

```
marioc:istio-1.5.2 arunsah$ kubectl apply -f ./install/kubernetes/istio-demo.yaml 
namespace/istio-system created
customresourcedefinition.apiextensions.k8s.io/meshpolicies.authentication.istio.io unchanged
customresourcedefinition.apiextensions.k8s.io/policies.authentication.istio.io unchanged
customresourcedefinition.apiextensions.k8s.io/httpapispecs.config.istio.io unchanged
customresourcedefinition.apiextensions.k8s.io/httpapispecbindings.config.istio.io unchanged
customresourcedefinition.apiextensions.k8s.io/quotaspecs.config.istio.io unchanged
customresourcedefinition.apiextensions.k8s.io/quotaspecbindings.config.istio.io unchanged
customresourcedefinition.apiextensions.k8s.io/destinationrules.networking.istio.io unchanged
customresourcedefinition.apiextensions.k8s.io/envoyfilters.networking.istio.io unchanged
customresourcedefinition.apiextensions.k8s.io/gateways.networking.istio.io unchanged
customresourcedefinition.apiextensions.k8s.io/serviceentries.networking.istio.io unchanged
customresourcedefinition.apiextensions.k8s.io/sidecars.networking.istio.io unchanged
customresourcedefinition.apiextensions.k8s.io/virtualservices.networking.istio.io unchanged
customresourcedefinition.apiextensions.k8s.io/attributemanifests.config.istio.io unchanged
customresourcedefinition.apiextensions.k8s.io/handlers.config.istio.io unchanged
customresourcedefinition.apiextensions.k8s.io/instances.config.istio.io unchanged
customresourcedefinition.apiextensions.k8s.io/rules.config.istio.io unchanged
customresourcedefinition.apiextensions.k8s.io/clusterrbacconfigs.rbac.istio.io unchanged
customresourcedefinition.apiextensions.k8s.io/rbacconfigs.rbac.istio.io unchanged
customresourcedefinition.apiextensions.k8s.io/serviceroles.rbac.istio.io unchanged
customresourcedefinition.apiextensions.k8s.io/servicerolebindings.rbac.istio.io unchanged
customresourcedefinition.apiextensions.k8s.io/authorizationpolicies.security.istio.io unchanged
customresourcedefinition.apiextensions.k8s.io/peerauthentications.security.istio.io unchanged
customresourcedefinition.apiextensions.k8s.io/requestauthentications.security.istio.io unchanged
customresourcedefinition.apiextensions.k8s.io/clusterissuers.certmanager.k8s.io unchanged
customresourcedefinition.apiextensions.k8s.io/issuers.certmanager.k8s.io unchanged
customresourcedefinition.apiextensions.k8s.io/certificates.certmanager.k8s.io unchanged
customresourcedefinition.apiextensions.k8s.io/orders.certmanager.k8s.io unchanged
customresourcedefinition.apiextensions.k8s.io/challenges.certmanager.k8s.io unchanged
customresourcedefinition.apiextensions.k8s.io/adapters.config.istio.io unchanged
customresourcedefinition.apiextensions.k8s.io/templates.config.istio.io unchanged
poddisruptionbudget.policy/istio-galley created
poddisruptionbudget.policy/istio-egressgateway created
poddisruptionbudget.policy/istio-ingressgateway created
poddisruptionbudget.policy/istio-policy created
poddisruptionbudget.policy/istio-telemetry created
poddisruptionbudget.policy/istio-pilot created
poddisruptionbudget.policy/istio-citadel created
poddisruptionbudget.policy/istio-sidecar-injector created
secret/kiali created
configmap/istio-galley-configuration created
configmap/istio-grafana-custom-resources created
configmap/istio-grafana-configuration-dashboards-citadel-dashboard created
configmap/istio-grafana-configuration-dashboards-galley-dashboard created
configmap/istio-grafana-configuration-dashboards-istio-mesh-dashboard created
configmap/istio-grafana-configuration-dashboards-istio-performance-dashboard created
configmap/istio-grafana-configuration-dashboards-istio-service-dashboard created
configmap/istio-grafana-configuration-dashboards-istio-workload-dashboard created
configmap/istio-grafana-configuration-dashboards-mixer-dashboard created
configmap/istio-grafana-configuration-dashboards-pilot-dashboard created
configmap/istio-grafana created
configmap/kiali created
configmap/prometheus created
configmap/istio-security-custom-resources created
configmap/istio created
configmap/istio-sidecar-injector created
serviceaccount/istio-galley-service-account created
serviceaccount/istio-egressgateway-service-account created
serviceaccount/istio-ingressgateway-service-account created
serviceaccount/istio-grafana-post-install-account created
clusterrole.rbac.authorization.k8s.io/istio-grafana-post-install-istio-system created
clusterrolebinding.rbac.authorization.k8s.io/istio-grafana-post-install-role-binding-istio-system created
job.batch/istio-grafana-post-install-1.5.2 created
serviceaccount/kiali-service-account created
serviceaccount/istio-mixer-service-account created
serviceaccount/istio-pilot-service-account created
serviceaccount/prometheus created
serviceaccount/istio-security-post-install-account created
clusterrole.rbac.authorization.k8s.io/istio-security-post-install-istio-system created
clusterrolebinding.rbac.authorization.k8s.io/istio-security-post-install-role-binding-istio-system created
job.batch/istio-security-post-install-1.5.2 created
serviceaccount/istio-citadel-service-account created
serviceaccount/istio-sidecar-injector-service-account created
serviceaccount/istio-multi created
serviceaccount/istio-reader-service-account created
clusterrole.rbac.authorization.k8s.io/istio-galley-istio-system created
clusterrole.rbac.authorization.k8s.io/kiali created
clusterrole.rbac.authorization.k8s.io/kiali-viewer created
clusterrole.rbac.authorization.k8s.io/istio-mixer-istio-system created
clusterrole.rbac.authorization.k8s.io/istio-pilot-istio-system created
clusterrole.rbac.authorization.k8s.io/prometheus-istio-system created
clusterrole.rbac.authorization.k8s.io/istio-citadel-istio-system created
clusterrole.rbac.authorization.k8s.io/istio-sidecar-injector-istio-system created
clusterrole.rbac.authorization.k8s.io/istio-reader created
clusterrolebinding.rbac.authorization.k8s.io/istio-galley-admin-role-binding-istio-system created
clusterrolebinding.rbac.authorization.k8s.io/istio-kiali-admin-role-binding-istio-system created
clusterrolebinding.rbac.authorization.k8s.io/istio-mixer-admin-role-binding-istio-system created
clusterrolebinding.rbac.authorization.k8s.io/istio-pilot-istio-system created
clusterrolebinding.rbac.authorization.k8s.io/prometheus-istio-system created
clusterrolebinding.rbac.authorization.k8s.io/istio-citadel-istio-system created
clusterrolebinding.rbac.authorization.k8s.io/istio-sidecar-injector-admin-role-binding-istio-system created
clusterrolebinding.rbac.authorization.k8s.io/istio-multi created
clusterrolebinding.rbac.authorization.k8s.io/istio-reader created
service/istio-galley created
service/istio-egressgateway created
service/istio-ingressgateway created
service/grafana created
service/kiali created
service/istio-policy created
service/istio-telemetry created
service/istio-pilot created
service/prometheus created
service/istio-citadel created
service/istio-sidecar-injector created
deployment.apps/istio-galley created
deployment.apps/istio-egressgateway created
deployment.apps/istio-ingressgateway created
deployment.apps/grafana created
deployment.apps/kiali created
deployment.apps/istio-policy created
deployment.apps/istio-telemetry created
deployment.apps/istio-pilot created
deployment.apps/prometheus created
deployment.apps/istio-citadel created
deployment.apps/istio-sidecar-injector created
deployment.apps/istio-tracing created
service/jaeger-query created
service/jaeger-collector created
service/jaeger-collector-headless created
service/jaeger-agent created
service/zipkin created
service/tracing created
mutatingwebhookconfiguration.admissionregistration.k8s.io/istio-sidecar-injector created
validatingwebhookconfiguration.admissionregistration.k8s.io/istio-galley created
attributemanifest.config.istio.io/istioproxy created
attributemanifest.config.istio.io/kubernetes created
handler.config.istio.io/stdio created
instance.config.istio.io/accesslog created
instance.config.istio.io/tcpaccesslog created
rule.config.istio.io/stdio created
rule.config.istio.io/stdiotcp created
instance.config.istio.io/requestcount created
instance.config.istio.io/requestduration created
instance.config.istio.io/requestsize created
instance.config.istio.io/responsesize created
instance.config.istio.io/tcpbytesent created
instance.config.istio.io/tcpbytereceived created
instance.config.istio.io/tcpconnectionsopened created
instance.config.istio.io/tcpconnectionsclosed created
handler.config.istio.io/prometheus created
rule.config.istio.io/promhttp created
rule.config.istio.io/promtcp created
rule.config.istio.io/promtcpconnectionopen created
rule.config.istio.io/promtcpconnectionclosed created
handler.config.istio.io/kubernetesenv created
rule.config.istio.io/kubeattrgenrulerule created
rule.config.istio.io/tcpkubeattrgenrulerule created
instance.config.istio.io/attributes created
destinationrule.networking.istio.io/istio-policy created
destinationrule.networking.istio.io/istio-telemetry created
marioc:istio-1.5.2 arunsah$ 
```

The above step results in the creation of a new namespace – `istio-system` – under which multiple objects get deployed.

```
marioc:istio-1.5.2 arunsah$ kubectl get ns
NAME              STATUS   AGE
default           Active   6d17h
docker            Active   6d17h
istio-system      Active   104s
kube-node-lease   Active   6d17h
kube-public       Active   6d17h
kube-system       Active   6d17h
marioc:istio-1.5.2 arunsah$ 
```

- multiple services created within the **istio-system**namespace
```
marioc:istio-1.5.2 arunsah$ kubectl get svc -n=istio-system -o wide
NAME                        TYPE        CLUSTER-IP       EXTERNAL-IP   PORT(S)                                                                                                                                      AGE     SELECTOR
grafana                     ClusterIP   10.109.7.134     <none>        3000/TCP                                                                                                                                     2m55s   app=grafana
istio-citadel               ClusterIP   10.103.172.230   <none>        8060/TCP,15014/TCP                                                                                                                           2m55s   istio=citadel
istio-egressgateway         ClusterIP   10.108.188.211   <none>        80/TCP,443/TCP,15443/TCP                                                                                                                     2m55s   app=istio-egressgateway,istio=egressgateway,release=istio
istio-galley                ClusterIP   10.110.158.212   <none>        443/TCP,15014/TCP,9901/TCP                                                                                                                   2m55s   istio=galley
istio-ingressgateway        NodePort    10.97.249.2      <none>        15020:32067/TCP,80:31380/TCP,443:31390/TCP,31400:31400/TCP,15029:31276/TCP,15030:31592/TCP,15031:30499/TCP,15032:32554/TCP,15443:32619/TCP   2m55s   app=istio-ingressgateway,istio=ingressgateway,release=istio
istio-pilot                 ClusterIP   10.107.95.34     <none>        15010/TCP,15011/TCP,8080/TCP,15014/TCP                                                                                                       2m55s   istio=pilot
istio-policy                ClusterIP   10.102.86.102    <none>        9091/TCP,15004/TCP,15014/TCP                                                                                                                 2m55s   istio-mixer-type=policy,istio=mixer
istio-sidecar-injector      ClusterIP   10.100.183.168   <none>        443/TCP,15014/TCP                                                                                                                            2m55s   istio=sidecar-injector
istio-telemetry             ClusterIP   10.96.118.172    <none>        9091/TCP,15004/TCP,15014/TCP,42422/TCP                                                                                                       2m55s   istio-mixer-type=telemetry,istio=mixer
jaeger-agent                ClusterIP   None             <none>        5775/UDP,6831/UDP,6832/UDP                                                                                                                   2m54s   app=jaeger
jaeger-collector            ClusterIP   10.103.42.252    <none>        14267/TCP,14268/TCP,14250/TCP                                                                                                                2m54s   app=jaeger
jaeger-collector-headless   ClusterIP   None             <none>        14250/TCP                                                                                                                                    2m54s   app=jaeger
jaeger-query                ClusterIP   10.98.29.240     <none>        16686/TCP                                                                                                                                    2m54s   app=jaeger
kiali                       ClusterIP   10.100.67.246    <none>        20001/TCP                                                                                                                                    2m55s   app=kiali
prometheus                  ClusterIP   10.98.221.225    <none>        9090/TCP                                                                                                                                     2m55s   app=prometheus
tracing                     ClusterIP   10.98.18.141     <none>        80/TCP                                                                                                                                       2m53s   app=jaeger
zipkin                      ClusterIP   10.107.40.96     <none>        9411/TCP                                                                                                                                     2m53s   app=jaeger
marioc:istio-1.5.2 arunsah$ 

marioc:istio-1.5.2 arunsah$ kubectl get svc -n=istio-system -o=custom-columns=NAME:.metadata.name,IP:.spec.clusterIP
NAME                        IP
grafana                     10.109.7.134
istio-citadel               10.103.172.230
istio-egressgateway         10.108.188.211
istio-galley                10.110.158.212
istio-ingressgateway        10.97.249.2
istio-pilot                 10.107.95.34
istio-policy                10.102.86.102
istio-sidecar-injector      10.100.183.168
istio-telemetry             10.96.118.172
jaeger-agent                None
jaeger-collector            10.103.42.252
jaeger-collector-headless   None
jaeger-query                10.98.29.240
kiali                       10.100.67.246
prometheus                  10.98.221.225
tracing                     10.98.18.141
zipkin                      10.107.40.96
marioc:istio-1.5.2 arunsah$ 

```



kubectl get events —all-namespaces  —sort-by=‘.metadata.creationTimestamp’

kubectl get events -n=istio-system  —sort-by=‘.metadata.creationTimestamp’
kubectl describe pod kiali-7ff568c949-t47l9  -n istio-system


- multiple pods deployed by Istio
```
marioc:istio-1.5.2 arunsah$ kubectl get pods -n=istio-system
NAME                                      READY   STATUS              RESTARTS   AGE
grafana-584949b9c6-wbpnm                  0/1     ImagePullBackOff    0          5m28s
istio-citadel-7998dbbd9c-npgnt            0/1     ImagePullBackOff    0          5m28s
istio-egressgateway-769fd9869f-rfvb7      0/1     ImagePullBackOff    0          5m29s
istio-galley-5cb68c8bdb-b9dr4             0/1     ContainerCreating   0          5m29s
istio-grafana-post-install-1.5.2-htwx5    0/1     ImagePullBackOff    0          5m30s
istio-ingressgateway-67c9b549cb-r8ls2     0/1     ImagePullBackOff    0          5m28s
istio-pilot-6d84c7c7d7-pt62v              0/2     ErrImagePull        0          5m28s
istio-policy-bd4db6dff-mdk9s              0/2     ErrImagePull        0          5m28s
istio-security-post-install-1.5.2-prkv2   0/1     ImagePullBackOff    0          5m30s
istio-sidecar-injector-69c57976b-wz4dx    0/1     ContainerCreating   0          5m28s
istio-telemetry-57fb5464f4-czp6d          0/2     ErrImagePull        0          5m28s
istio-tracing-68ffb9d456-lg4wt            0/1     ImagePullBackOff    0          5m27s
kiali-7d4cf866cc-hgz7l                    0/1     ImagePullBackOff    0          5m28s
prometheus-8685f659f-4bbrn                0/1     ContainerCreating   0          5m28s
marioc:istio-1.5.2 arunsah$ 
```

**All the pods STATUS must be in running or complete mode, which indicates that Istio is successfully installed and configured.**

kubectl describe pod kiali-7ff568c949-t47l9  -n istio-system

```
$ kubectl get events -n=istio-system  —sort-by=‘.metadata.creationTimestamp’
Error from server (NotFound): events "—sort-by=‘.metadata.creationTimestamp’" not found
marioc:istio-1.5.2 arunsah$ kubectl get events -n=istio-system 
LAST SEEN   TYPE      REASON              OBJECT                                        MESSAGE
12m         Normal    Scheduled           pod/grafana-584949b9c6-8fjsz                  Successfully assigned istio-system/grafana-584949b9c6-8fjsz to docker-desktop
12m         Warning   FailedMount         pod/grafana-584949b9c6-8fjsz                  MountVolume.SetUp failed for volume "dashboards-istio-citadel-dashboard" : couldn't propagate object cache: timed out waiting for the condition
12m         Warning   FailedMount         pod/grafana-584949b9c6-8fjsz                  MountVolume.SetUp failed for volume "dashboards-istio-pilot-dashboard" : couldn't propagate object cache: timed out waiting for the condition
12m         Warning   FailedMount         pod/grafana-584949b9c6-8fjsz                  MountVolume.SetUp failed for volume "config" : couldn't propagate object cache: timed out waiting for the condition
12m         Warning   FailedMount         pod/grafana-584949b9c6-8fjsz                  MountVolume.SetUp failed for volume "dashboards-istio-istio-workload-dashboard" : couldn't propagate object cache: timed out waiting for the condition
12m         Warning   FailedMount         pod/grafana-584949b9c6-8fjsz                  MountVolume.SetUp failed for volume "dashboards-istio-istio-performance-dashboard" : couldn't propagate object cache: timed out waiting for the condition
12m         Warning   FailedMount         pod/grafana-584949b9c6-8fjsz                  MountVolume.SetUp failed for volume "default-token-hgsmm" : couldn't propagate object cache: timed out waiting for the condition
12m         Warning   FailedMount         pod/grafana-584949b9c6-8fjsz                  MountVolume.SetUp failed for volume "dashboards-istio-istio-service-dashboard" : couldn't propagate object cache: timed out waiting for the condition
12m         Warning   FailedMount         pod/grafana-584949b9c6-8fjsz                  MountVolume.SetUp failed for volume "dashboards-istio-mixer-dashboard" : couldn't propagate object cache: timed out waiting for the condition
12m         Warning   FailedMount         pod/grafana-584949b9c6-8fjsz                  MountVolume.SetUp failed for volume "dashboards-istio-galley-dashboard" : couldn't propagate object cache: timed out waiting for the condition
12m         Warning   FailedMount         pod/grafana-584949b9c6-8fjsz                  (combined from similar events): MountVolume.SetUp failed for volume "dashboards-istio-istio-mesh-dashboard" : couldn't propagate object cache: timed out waiting for the condition
12m         Warning   FailedMount         pod/grafana-584949b9c6-8fjsz                  MountVolume.SetUp failed for volume "dashboards-istio-istio-mesh-dashboard" : couldn't propagate object cache: timed out waiting for the condition
12m         Normal    Pulling             pod/grafana-584949b9c6-8fjsz                  Pulling image "grafana/grafana:6.4.3"
12m         Normal    SuccessfulCreate    replicaset/grafana-584949b9c6                 Created pod: grafana-584949b9c6-8fjsz
12m         Normal    ScalingReplicaSet   deployment/grafana                            Scaled up replica set grafana-584949b9c6 to 1
12m         Normal    Scheduled           pod/istio-citadel-7998dbbd9c-dh2zn            Successfully assigned istio-system/istio-citadel-7998dbbd9c-dh2zn to docker-desktop
12m         Warning   FailedMount         pod/istio-citadel-7998dbbd9c-dh2zn            MountVolume.SetUp failed for volume "istio-citadel-service-account-token-cjc2h" : couldn't propagate object cache: timed out waiting for the condition
12m         Normal    Pulling             pod/istio-citadel-7998dbbd9c-dh2zn            Pulling image "docker.io/istio/citadel:1.5.2"
12m         Normal    SuccessfulCreate    replicaset/istio-citadel-7998dbbd9c           Created pod: istio-citadel-7998dbbd9c-dh2zn
12m         Normal    NoPods              poddisruptionbudget/istio-citadel             No matching pods found
12m         Normal    ScalingReplicaSet   deployment/istio-citadel                      Scaled up replica set istio-citadel-7998dbbd9c to 1
12m         Normal    Scheduled           pod/istio-egressgateway-769fd9869f-nfdch      Successfully assigned istio-system/istio-egressgateway-769fd9869f-nfdch to docker-desktop
12m         Normal    Pulling             pod/istio-egressgateway-769fd9869f-nfdch      Pulling image "docker.io/istio/proxyv2:1.5.2"
12m         Normal    SuccessfulCreate    replicaset/istio-egressgateway-769fd9869f     Created pod: istio-egressgateway-769fd9869f-nfdch
12m         Normal    NoPods              poddisruptionbudget/istio-egressgateway       No matching pods found
12m         Normal    ScalingReplicaSet   deployment/istio-egressgateway                Scaled up replica set istio-egressgateway-769fd9869f to 1
12m         Normal    Scheduled           pod/istio-galley-5cb68c8bdb-crlvx             Successfully assigned istio-system/istio-galley-5cb68c8bdb-crlvx to docker-desktop
3s          Warning   FailedMount         pod/istio-galley-5cb68c8bdb-crlvx             MountVolume.SetUp failed for volume "certs" : secret "istio.istio-galley-service-account" not found
75s         Warning   FailedMount         pod/istio-galley-5cb68c8bdb-crlvx             Unable to mount volumes for pod "istio-galley-5cb68c8bdb-crlvx_istio-system(8d4605f7-bab4-4668-bd8d-a9932d8e0a70)": timeout expired waiting for volumes to attach or mount for pod "istio-system"/"istio-galley-5cb68c8bdb-crlvx". list of unmounted volumes=[certs]. list of unattached volumes=[certs config mesh-config istio-galley-service-account-token-r9kk9]
12m         Normal    SuccessfulCreate    replicaset/istio-galley-5cb68c8bdb            Created pod: istio-galley-5cb68c8bdb-crlvx
12m         Normal    NoPods              poddisruptionbudget/istio-galley              No matching pods found
12m         Normal    ScalingReplicaSet   deployment/istio-galley                       Scaled up replica set istio-galley-5cb68c8bdb to 1
12m         Normal    Scheduled           pod/istio-grafana-post-install-1.5.2-5n7pp    Successfully assigned istio-system/istio-grafana-post-install-1.5.2-5n7pp to docker-desktop
12m         Normal    Pulling             pod/istio-grafana-post-install-1.5.2-5n7pp    Pulling image "docker.io/istio/kubectl:1.5.2"
5s          Normal    Pulled              pod/istio-grafana-post-install-1.5.2-5n7pp    Successfully pulled image "docker.io/istio/kubectl:1.5.2"
4s          Normal    Created             pod/istio-grafana-post-install-1.5.2-5n7pp    Created container kubectl
3s          Normal    Started             pod/istio-grafana-post-install-1.5.2-5n7pp    Started container kubectl
4s          Normal    Pulled              pod/istio-grafana-post-install-1.5.2-5n7pp    Container image "docker.io/istio/kubectl:1.5.2" already present on machine
2s          Warning   BackOff             pod/istio-grafana-post-install-1.5.2-5n7pp    Back-off restarting failed container
12m         Normal    SuccessfulCreate    job/istio-grafana-post-install-1.5.2          Created pod: istio-grafana-post-install-1.5.2-5n7pp
12m         Normal    Scheduled           pod/istio-ingressgateway-67c9b549cb-h7gtw     Successfully assigned istio-system/istio-ingressgateway-67c9b549cb-h7gtw to docker-desktop
12m         Warning   FailedMount         pod/istio-ingressgateway-67c9b549cb-h7gtw     MountVolume.SetUp failed for volume "istio-ingressgateway-service-account-token-v2r4d" : couldn't propagate object cache: timed out waiting for the condition
12m         Warning   FailedMount         pod/istio-ingressgateway-67c9b549cb-h7gtw     MountVolume.SetUp failed for volume "istio-certs" : couldn't propagate object cache: timed out waiting for the condition
12m         Warning   FailedMount         pod/istio-ingressgateway-67c9b549cb-h7gtw     MountVolume.SetUp failed for volume "ingressgateway-certs" : couldn't propagate object cache: timed out waiting for the condition
12m         Normal    Pulling             pod/istio-ingressgateway-67c9b549cb-h7gtw     Pulling image "docker.io/istio/proxyv2:1.5.2"
12m         Normal    SuccessfulCreate    replicaset/istio-ingressgateway-67c9b549cb    Created pod: istio-ingressgateway-67c9b549cb-h7gtw
12m         Normal    NoPods              poddisruptionbudget/istio-ingressgateway      No matching pods found
12m         Normal    ScalingReplicaSet   deployment/istio-ingressgateway               Scaled up replica set istio-ingressgateway-67c9b549cb to 1
12m         Normal    Scheduled           pod/istio-pilot-6d84c7c7d7-tpwtb              Successfully assigned istio-system/istio-pilot-6d84c7c7d7-tpwtb to docker-desktop
12m         Warning   FailedMount         pod/istio-pilot-6d84c7c7d7-tpwtb              MountVolume.SetUp failed for volume "istio-certs" : couldn't propagate object cache: timed out waiting for the condition
12m         Warning   FailedMount         pod/istio-pilot-6d84c7c7d7-tpwtb              MountVolume.SetUp failed for volume "istio-pilot-service-account-token-8x6fv" : couldn't propagate object cache: timed out waiting for the condition
12m         Normal    Pulling             pod/istio-pilot-6d84c7c7d7-tpwtb              Pulling image "docker.io/istio/pilot:1.5.2"
12m         Normal    SuccessfulCreate    replicaset/istio-pilot-6d84c7c7d7             Created pod: istio-pilot-6d84c7c7d7-tpwtb
12m         Normal    NoPods              poddisruptionbudget/istio-pilot               No matching pods found
12m         Normal    ScalingReplicaSet   deployment/istio-pilot                        Scaled up replica set istio-pilot-6d84c7c7d7 to 1
12m         Normal    Scheduled           pod/istio-policy-bd4db6dff-xh6sq              Successfully assigned istio-system/istio-policy-bd4db6dff-xh6sq to docker-desktop
12m         Warning   FailedMount         pod/istio-policy-bd4db6dff-xh6sq              MountVolume.SetUp failed for volume "istio-mixer-service-account-token-grhtl" : couldn't propagate object cache: timed out waiting for the condition
12m         Warning   FailedMount         pod/istio-policy-bd4db6dff-xh6sq              MountVolume.SetUp failed for volume "istio-certs" : couldn't propagate object cache: timed out waiting for the condition
12m         Warning   FailedMount         pod/istio-policy-bd4db6dff-xh6sq              MountVolume.SetUp failed for volume "policy-adapter-secret" : couldn't propagate object cache: timed out waiting for the condition
12m         Normal    Pulling             pod/istio-policy-bd4db6dff-xh6sq              Pulling image "docker.io/istio/mixer:1.5.2"
12m         Normal    SuccessfulCreate    replicaset/istio-policy-bd4db6dff             Created pod: istio-policy-bd4db6dff-xh6sq
12m         Normal    NoPods              poddisruptionbudget/istio-policy              No matching pods found
12m         Normal    ScalingReplicaSet   deployment/istio-policy                       Scaled up replica set istio-policy-bd4db6dff to 1
12m         Normal    Scheduled           pod/istio-security-post-install-1.5.2-4b9hc   Successfully assigned istio-system/istio-security-post-install-1.5.2-4b9hc to docker-desktop
11m         Normal    Pulling             pod/istio-security-post-install-1.5.2-4b9hc   Pulling image "docker.io/istio/kubectl:1.5.2"
12m         Warning   Failed              pod/istio-security-post-install-1.5.2-4b9hc   Failed to pull image "docker.io/istio/kubectl:1.5.2": rpc error: code = Unknown desc = error pulling image configuration: Get https://production.cloudflare.docker.com/registry-v2/docker/registry/v2/blobs/sha256/9a/9acff496f04763983d60d7b1daf682af3f95127456f948a094a12b85c086b653/data?verify=1588669193-6R9wsvO2nUInWthAIrau74Flz4s%3D: net/http: TLS handshake timeout
12m         Warning   Failed              pod/istio-security-post-install-1.5.2-4b9hc   Error: ErrImagePull
12m         Normal    SandboxChanged      pod/istio-security-post-install-1.5.2-4b9hc   Pod sandbox changed, it will be killed and re-created.
12m         Normal    BackOff             pod/istio-security-post-install-1.5.2-4b9hc   Back-off pulling image "docker.io/istio/kubectl:1.5.2"
12m         Warning   Failed              pod/istio-security-post-install-1.5.2-4b9hc   Error: ImagePullBackOff
12m         Normal    SuccessfulCreate    job/istio-security-post-install-1.5.2         Created pod: istio-security-post-install-1.5.2-4b9hc
12m         Normal    Scheduled           pod/istio-sidecar-injector-69c57976b-29glt    Successfully assigned istio-system/istio-sidecar-injector-69c57976b-29glt to docker-desktop
12m         Warning   FailedMount         pod/istio-sidecar-injector-69c57976b-29glt    MountVolume.SetUp failed for volume "istio-sidecar-injector-service-account-token-pfhsk" : couldn't propagate object cache: timed out waiting for the condition
12m         Warning   FailedMount         pod/istio-sidecar-injector-69c57976b-29glt    MountVolume.SetUp failed for volume "certs" : couldn't propagate object cache: timed out waiting for the condition
12m         Warning   FailedMount         pod/istio-sidecar-injector-69c57976b-29glt    MountVolume.SetUp failed for volume "inject-config" : couldn't propagate object cache: timed out waiting for the condition
2m1s        Warning   FailedMount         pod/istio-sidecar-injector-69c57976b-29glt    MountVolume.SetUp failed for volume "certs" : secret "istio.istio-sidecar-injector-service-account" not found
75s         Warning   FailedMount         pod/istio-sidecar-injector-69c57976b-29glt    Unable to mount volumes for pod "istio-sidecar-injector-69c57976b-29glt_istio-system(f9510c51-02a1-4da4-970a-3567070df204)": timeout expired waiting for volumes to attach or mount for pod "istio-system"/"istio-sidecar-injector-69c57976b-29glt". list of unmounted volumes=[certs]. list of unattached volumes=[config-volume certs inject-config istio-sidecar-injector-service-account-token-pfhsk]
12m         Normal    SuccessfulCreate    replicaset/istio-sidecar-injector-69c57976b   Created pod: istio-sidecar-injector-69c57976b-29glt
12m         Normal    NoPods              poddisruptionbudget/istio-sidecar-injector    No matching pods found
12m         Normal    ScalingReplicaSet   deployment/istio-sidecar-injector             Scaled up replica set istio-sidecar-injector-69c57976b to 1
12m         Normal    Scheduled           pod/istio-telemetry-57fb5464f4-prbjp          Successfully assigned istio-system/istio-telemetry-57fb5464f4-prbjp to docker-desktop
12m         Warning   FailedMount         pod/istio-telemetry-57fb5464f4-prbjp          MountVolume.SetUp failed for volume "istio-mixer-service-account-token-grhtl" : couldn't propagate object cache: timed out waiting for the condition
12m         Warning   FailedMount         pod/istio-telemetry-57fb5464f4-prbjp          MountVolume.SetUp failed for volume "telemetry-adapter-secret" : couldn't propagate object cache: timed out waiting for the condition
12m         Warning   FailedMount         pod/istio-telemetry-57fb5464f4-prbjp          MountVolume.SetUp failed for volume "istio-certs" : couldn't propagate object cache: timed out waiting for the " : couldn't propagate object cache: timed out waiting for the condition
12m         Normal    Pulling             pod/istio-telemetry-57fb5464f4-prbjp          Pulling image "docker.io/istio/mixer:1.5.2"
12m         Normal    SuccessfulCreate    replicaset/istio-telemetry-57fb5464f4         Created pod: istio-telemetry-57fb5464f4-prbjp
12m         Normal    NoPods              poddisruptionbudget/istio-telemetry           No matching pods found
12m         Normal    ScalingReplicaSet   deployment/istio-telemetry                    Scaled up replica set istio-telemetry-57fb5464f4 to 1
12m         Normal    Scheduled           pod/istio-tracing-68ffb9d456-xsrrq            Successfully assigned istio-system/istio-tracing-68ffb9d456-xsrrq to docker-desktop
12m         Normal    Pulling             pod/istio-tracing-68ffb9d456-xsrrq            Pulling image “docker.io/jaegertracing/all-in-one:1.16”
12m         Normal    SuccessfulCreate    replicaset/istio-tracing-68ffb9d456           Created pod: istio-tracing-68ffb9d456-xsrrq
12m         Normal    ScalingReplicaSet   deployment/istio-tracing                      Scaled up replica set istio-tracing-68ffb9d456 to 1
12m         Normal    Scheduled           pod/kiali-7d4cf866cc-tr2hv                    Successfully assigned istio-system/kiali-7d4cf866cc-tr2hv to docker-desktop
12m         Warning   FailedMount         pod/kiali-7d4cf866cc-tr2hv                    MountVolume.SetUp failed for volume “kiali-cert” : couldn’t propagate object cache: timed out waiting for the condition
12m         Warning   FailedMount         pod/kiali-7d4cf866cc-tr2hv                    MountVolume.SetUp failed for volume “kiali-secret” : couldn’t propagate object cache: timed out waiting for the condition
12m         Warning   FailedMount         pod/kiali-7d4cf866cc-tr2hv                    MountVolume.SetUp failed for volume “kiali-configuration” : couldn’t propagate object cache: timed out waiting for the condition
12m         Warning   FailedMount         pod/kiali-7d4cf866cc-tr2hv                    MountVolume.SetUp failed for volume “kiali-service-account-token-2vm7f” : couldn’t propagate object cache: timed out waiting for the condition
12m         Normal    Pulling             pod/kiali-7d4cf866cc-tr2hv                    Pulling image “quay.io/kiali/kiali:v1.9”
12m         Normal    SuccessfulCreate    replicaset/kiali-7d4cf866cc                   Created pod: kiali-7d4cf866cc-tr2hv
12m         Normal    ScalingReplicaSet   deployment/kiali                              Scaled up replica set kiali-7d4cf866cc to 1
12m         Normal    Scheduled           pod/prometheus-8685f659f-kt67s                Successfully assigned istio-system/prometheus-8685f659f-kt67s to docker-desktop
12m         Warning   FailedMount         pod/prometheus-8685f659f-kt67s                MountVolume.SetUp failed for volume “istio-certs” : couldn’t propagate object cache: timed out waiting for the condition
12m         Warning   FailedMount         pod/prometheus-8685f659f-kt67s                MountVolume.SetUp failed for volume “config-volume” : couldn’t propagate object cache: timed out waiting for the condition
12m         Warning   FailedMount         pod/prometheus-8685f659f-kt67s                MountVolume.SetUp failed for volume “prometheus-token-4tscq” : couldn’t propagate object cache: timed out waiting for the condition
2m1s        Warning   FailedMount         pod/prometheus-8685f659f-kt67s                MountVolume.SetUp failed for volume “istio-certs” : secret “istio.default” not found
70s         Warning   FailedMount         pod/prometheus-8685f659f-kt67s                Unable to mount volumes for pod “prometheus-8685f659f-kt67s_istio-system(5104545b-d422-4190-ba2a-634d9e9e6680)”: timeout expired waiting for volumes to attach or mount for pod “istio-system”/“prometheus-8685f659f-kt67s”. list of unmounted volumes=[istio-certs]. list of unattached volumes=[config-volume istio-certs prometheus-token-4tscq]
12m         Normal    SuccessfulCreate    replicaset/prometheus-8685f659f               Created pod: prometheus-8685f659f-kt67s
12m         Normal    ScalingReplicaSet   deployment/prometheus                         Scaled up replica set prometheus-8685f659f to 1
marioc:istio-1.5.2 arunsah$ 

```

kubectl delete namespaces istio-system
$ kubectl delete -f  [samples/bookinfo/networking/virtual-service-all-v1.yaml](https://raw.githubusercontent.com/istio/istio/release-1.5/samples/bookinfo/networking/virtual-service-all-v1.yaml) 
- [ ] 

kubectl describe pod xxx  -n istio-system
kubectl describe pod kiali-7d4cf866cc-tr2hv  -n istio-system
kubectl describe pod grafana-584949b9c6-8fjsz    -n istio-system
kubectl describe pod istio-citadel-7998dbbd9c-dh2zn  -n istio-system
kubectl describe pod xxx  -n istio-system
kubectl describe pod xxx  -n istio-system
kubectl describe pod xxx  -n istio-system
kubectl describe pod xxx  -n istio-system
kubectl describe pod xxx  -n istio-system
kubectl describe pod xxx  -n istio-system
kubectl describe pod xxx  -n istio-system

```
marioc:istio-1.5.2 arunsah$ kubectl get pods -n=istio-system
NAME                                      READY   STATUS              RESTARTS   AGE
grafana-584949b9c6-8fjsz                  0/1     ImagePullBackOff    0          29m
istio-citadel-7998dbbd9c-dh2zn            0/1     ContainerCreating   0          29m
istio-egressgateway-769fd9869f-nfdch      0/1     ImagePullBackOff    0          29m
istio-galley-5cb68c8bdb-crlvx             0/1     ContainerCreating   0          29m
istio-ingressgateway-67c9b549cb-h7gtw     0/1     ImagePullBackOff    0          29m
istio-pilot-6d84c7c7d7-tpwtb              0/2     ContainerCreating   0          29m
istio-policy-bd4db6dff-xh6sq              0/2     ContainerCreating   0          29m
istio-security-post-install-1.5.2-4b9hc   0/1     ImagePullBackOff    0          29m
istio-sidecar-injector-69c57976b-29glt    0/1     ContainerCreating   0          29m
istio-telemetry-57fb5464f4-prbjp          0/2     ContainerCreating   0          29m
istio-tracing-68ffb9d456-xsrrq            0/1     ImagePullBackOff    0          29m
kiali-7d4cf866cc-tr2hv                    1/1     Running             0          29m
prometheus-8685f659f-kt67s                0/1     ContainerCreating   0          29m
```

*Describe each of these image which got failed and try to pull the image separately. 



```
marioc:istio-1.5.2 arunsah$ kubectl apply -f ./install/kubernetes/helm/istio-init/files
marioc:istio-1.5.2 arunsah$ kubectl apply -f ./install/kubernetes/istio-demo.yaml

marioc:istio-1.5.2 arunsah$ kubectl get pods -n=istio-system
NAME                                      READY   STATUS      RESTARTS   AGE
grafana-584949b9c6-rs25v                  1/1     Running     0          67s
istio-citadel-7998dbbd9c-x4kmd            1/1     Running     0          66s
istio-egressgateway-769fd9869f-vrk4z      0/1     Running     0          67s
istio-galley-5cb68c8bdb-tsk6h             1/1     Running     0          67s
istio-grafana-post-install-1.5.2-lb4wg    0/1     Completed   0          68s
istio-ingressgateway-67c9b549cb-8p2r8     0/1     Running     0          67s
istio-pilot-6d84c7c7d7-kxf5d              2/2     Running     2          67s
istio-policy-bd4db6dff-2x2kl              2/2     Running     1          67s
istio-security-post-install-1.5.2-tg6sq   0/1     Completed   0          68s
istio-sidecar-injector-69c57976b-xcz7h    1/1     Running     0          66s
istio-telemetry-57fb5464f4-ljr47          2/2     Running     1          67s
istio-tracing-68ffb9d456-dnzpq            1/1     Running     0          66s
kiali-7d4cf866cc-9dllr                    1/1     Running     0          67s
prometheus-8685f659f-m6gjl                1/1     Running     0          66s
marioc:istio-1.5.2 arunsah$ 


```

#### Step 3: Deploying two versions of the same application



```

apiVersion: v1
kind: Service
metadata:
  name: myapp
  labels:
    app: myapp
spec:
  type: ClusterIP
  ports:
  - port: 80
    name: http
  selector:
    app: myapp
---
apiVersion: extensions/v1beta1
kind: Deployment
metadata:
  name: myapp-v1
spec:
  replicas: 1
  template:
    metadata:
      labels:
        app: myapp
        version: v1
    spec:
      containers:
      - name: myapp
        image: janakiramm/myapp:v1
        imagePullPolicy: IfNotPresent
        ports:
        - containerPort: 80
---
apiVersion: extensions/v1beta1
kind: Deployment
metadata:
  name: myapp-v2
spec:
  replicas: 1
  template:
    metadata:
      labels:
        app: myapp
        version: v2
    spec:
      containers:
      - name: myapp
        image: janakiramm/myapp:v2
        imagePullPolicy: IfNotPresent
        ports:
        - containerPort: 80

```


Let’s start by creating a YAML file that defines the deployments for V1 and V2 along with a ClusterIP that exposes them. Notice the labels used for identifying the pods – app and version. While the app name remains the same the version is different between the two deployments.
This is expected by Istio to treat them as a single app but to differentiate them based on the version.
Same is the case with the ClusterIP service definition. Due the label, app: myapp, it is associated with the pods from both the deployments based on different versions.


```
marioc:janakiramm-myapp-demo arunsah$ pwd
/Users/arunsah/bin/istio/janakiramm-myapp-demo
marioc:janakiramm-myapp-demo arunsah$ ls
janakiramm-myapp.yaml
marioc:janakiramm-myapp-demo arunsah$ kubectl apply -f janakiramm-myapp.yaml 
service/myapp created
deployment.extensions/myapp-v1 created
deployment.extensions/myapp-v2 created
marioc:janakiramm-myapp-demo arunsah$ 
```


```
kubectl port-forward deployment/myapp-v1 8880:80
kubectl port-forward deployment/myapp-v2 8881:80
```


### Step 4: Configuring Blue/Green Deployments

Our goal is to drive the traffic selectively to one of the deployments with no downtime. To achieve this, we need to tell Istio to route the traffic based on the weights.

**Gateway**
An Istio Gateway describes a load balancer operating at the edge of the mesh receiving incoming or outgoing HTTP/TCP connections. The specification describes a set of ports that should be exposed, the type of protocol to use, SNI configuration for the load balancer, etc. In the below definition, we are pointing the gateway to the default Ingress Gateway created by Istio during the installation.

```
apiVersion: networking.istio.io/v1alpha3
kind: Gateway
metadata:
  name: app-gateway
spec:
  selector:
    istio: ingressgateway
  servers:
  - port:
      number: 80
      name: http
      protocol: HTTP
    hosts:
    - "*"

```


**Destination Rule**
An Istio DestinationRule defines policies that apply to traffic intended for a service after routing has occurred. Notice how the rule is declared based on the labels defined in the original Kubernetes deployment.

```
apiVersion: networking.istio.io/v1alpha3
kind: DestinationRule
metadata:
  name: myapp
spec:
  host: myapp
  subsets:
  - name: v1
    labels:
      version: v1
  - name: v2
    labels:
      version: v2

```


**Virtual Service**
A VirtualService defines a set of traffic routing rules to apply when a host is addressed. Each routing rule defines matching criteria for traffic of a specific protocol. If the traffic is matched, then it is sent to a named destination service based on a version.

```
apiVersion: networking.istio.io/v1alpha3
kind: VirtualService
metadata:
  name: myapp
spec:
  hosts:
  - "*"
  gateways:
  - app-gateway
  http:
    - route:
      - destination:
          host: myapp
          subset: v1
        weight: 60
      - destination:
          host: myapp
          subset: v2
        weight: 40  

```


### All Services

```
apiVersion: networking.istio.io/v1alpha3
kind: Gateway
metadata:
  name: app-gateway
spec:
  selector:
    istio: ingressgateway 
  servers:
  - port:
      number: 80
      name: http
      protocol: HTTP
    hosts:
    - "*"
---
apiVersion: networking.istio.io/v1alpha3
kind: DestinationRule
metadata:
  name: myapp
spec:
  host: myapp
  subsets:
  - name: v1
    labels:
      version: v1
  - name: v2
    labels:
      version: v2
---      
apiVersion: networking.istio.io/v1alpha3
kind: VirtualService
metadata:
  name: myapp
spec:
  hosts:
  - "*"
  gateways:
  - app-gateway
  http:
    - route:
      - destination:
          host: myapp
          subset: v1
        weight: 80
      - destination:
          host: myapp
          subset: v2
        weight: 20        
---

```



```
marioc:janakiramm-myapp-demo arunsah$ pwd
/Users/arunsah/bin/istio/janakiramm-myapp-demo
marioc:janakiramm-myapp-demo arunsah$ ls
janakiramm-myapp.yaml
marioc:janakiramm-myapp-demo arunsah$ kubectl apply -f janakiramm-myapp.yaml 
service/myapp created
deployment.extensions/myapp-v1 created
deployment.extensions/myapp-v2 created
marioc:janakiramm-myapp-demo arunsah$ kubectl apply -f janakiramm-all-svc.yaml 
gateway.networking.istio.io/app-gateway created
destinationrule.networking.istio.io/myapp created
virtualservice.networking.istio.io/myapp created
marioc:janakiramm-myapp-demo arunsah$ 


```



Run the below commands to access the Ingress Host (Minikube) and Ingress port.
```
$ export INGRESS_HOST=$(minikube ip)
 
$ export INGRESS_PORT=$(kubectl -n istio-system get service istio-ingressgateway -o jsonpath=‘{.spec.ports[?(@.name=="http2")].nodePort}’)


$ kubectl -n istio-system get service istio-ingressgateway -o jsonpath=‘{.spec.ports[?(@.name=="http2")].nodePort}’

while : ;do export GREP_COLOR='1;33';curl -s  192.168.99.100:31380 \
 |  grep --color=always "V1" ; export GREP_COLOR='1;36';\
 curl -s  192.168.99.100:31380 \
 | grep --color=always "vNext" ; sleep 1; done

---


marioc:janakiramm-myapp-demo arunsah$ kubectl -n istio-system get service istio-ingressgateway
NAME                   TYPE       CLUSTER-IP      EXTERNAL-IP   PORT(S)                                                                                                                                      AGE
istio-ingressgateway   NodePort   10.100.50.121   <none>        15020:30406/TCP,80:31380/TCP,443:31390/TCP,31400:31400/TCP,15029:31088/TCP,15030:30273/TCP,15031:30982/TCP,15032:31984/TCP,15443:31166/TCP   36m
marioc:janakiramm-myapp-demo arunsah$ 



while : ;do export GREP_COLOR='1;33';curl -s  localhost:31380 \
 |  grep --color=always "V1" ; export GREP_COLOR='1;36';\
 curl -s  localhost:31380 \
 | grep --color=always "vNext" ; sleep 1; done


```
If you access the URI from the browser, you will see the traffic getting routed evenly between blue and green pages.
We can see the result from a terminal window. Run the below command from the terminal window to see alternating response from V1 and V2.

```
marioc:janakiramm-myapp-demo arunsah$ while : ;do export GREP_COLOR='1;33';curl -s  localhost:31380 \
>  |  grep --color=always "V1" ; export GREP_COLOR='1;36';\
>  curl -s  localhost:31380 \
>  | grep --color=always "vNext" ; sleep 1; done
    <h1>Welcome to **V1** of the web application</h1>

    <h1>Welcome to **V1** of the web application</h1>
    <h1>Welcome to **vNext** of the web application</h1>
    <h1>Welcome to **V1** of the web application</h1>
    <h1>Welcome to **vNext** of the web application</h1>
    <h1>Welcome to **V1** of the web application</h1>
    <h1>Welcome to **V1** of the web application</h1>
    <h1>Welcome to **vNext** of the web application</h1>
    <h1>Welcome to **V1** of the web application</h1>
    <h1>Welcome to **V1** of the web application</h1>
    <h1>Welcome to **V1** of the web application</h1>
    <h1>Welcome to **V1** of the web application</h1>
    <h1>Welcome to **vNext** of the web application</h1>
    <h1>Welcome to **V1** of the web application</h1>
    <h1>Welcome to **V1** of the web application</h1>
    <h1>Welcome to **V1** of the web application</h1>
    <h1>Welcome to **V1** of the web application</h1>
    <h1>Welcome to **V1** of the web application</h1>
    <h1>Welcome to **vNext** of the web application</h1>
    <h1>Welcome to **V1** of the web application</h1>
    <h1>Welcome to **vNext** of the web application</h1>
    <h1>Welcome to **vNext** of the web application</h1>
    <h1>Welcome to **vNext** of the web application</h1>
    <h1>Welcome to **V1** of the web application</h1>
    <h1>Welcome to **vNext** of the web application</h1>
    <h1>Welcome to **V1** of the web application</h1>
    <h1>Welcome to **vNext** of the web application</h1>
^C
marioc:janakiramm-myapp-demo arunsah$ 

// change the weight

marioc:janakiramm-myapp-demo arunsah$ kubectl apply -f janakiramm-all-svc.yaml 
gateway.networking.istio.io/app-gateway unchanged
destinationrule.networking.istio.io/myapp unchanged
virtualservice.networking.istio.io/myapp configured



marioc:janakiramm-myapp-demo arunsah$ while : ;do export GREP_COLOR='1;33';curl -s  localhost:31380 \
>  |  grep --color=always "V1" ; export GREP_COLOR='1;36';\
>  curl -s  localhost:31380 \
>  | grep --color=always "vNext" ; sleep 1; done
    <h1>Welcome to vNext of the web application</h1>
    <h1>Welcome to vNext of the web application</h1>
    <h1>Welcome to vNext of the web application</h1>
    <h1>Welcome to V1 of the web application</h1>
    <h1>Welcome to vNext of the web application</h1>
    <h1>Welcome to vNext of the web application</h1>
    <h1>Welcome to vNext of the web application</h1>
    <h1>Welcome to V1 of the web application</h1>
    <h1>Welcome to vNext of the web application</h1>
    <h1>Welcome to vNext of the web application</h1>
    <h1>Welcome to V1 of the web application</h1>
    <h1>Welcome to vNext of the web application</h1>
    <h1>Welcome to vNext of the web application</h1>
    <h1>Welcome to vNext of the web application</h1>
    <h1>Welcome to vNext of the web application</h1>
    <h1>Welcome to vNext of the web application</h1>
    <h1>Welcome to vNext of the web application</h1>
    <h1>Welcome to vNext of the web application</h1>
    <h1>Welcome to vNext of the web application</h1>
    <h1>Welcome to vNext of the web application</h1>
    <h1>Welcome to vNext of the web application</h1>
    <h1>Welcome to vNext of the web application</h1>
    <h1>Welcome to vNext of the web application</h1>
    <h1>Welcome to vNext of the web application</h1>
    <h1>Welcome to vNext of the web application</h1>
    <h1>Welcome to vNext of the web application</h1>
    <h1>Welcome to vNext of the web application</h1>
    <h1>Welcome to vNext of the web application</h1>
    <h1>Welcome to vNext of the web application</h1>
^C
marioc:janakiramm-myapp-demo arunsah$ 

```

While the above command is running in a loop, let’s go back to the app-gateway.yaml file to adjust the weights. Set the weight of V1 to 0 and V2 to 100.
Submit the new definition to Istio.


```
$ istioctl replace -f app-gateway.yaml
```

Immediately after updating the weights, V2 will get 100 percent of the traffic. This is visible from the output of the first terminal window.


### References
- [Tutorial Blue Green Deployments With Kubernetes And Istio](https://thenewstack.io/tutorial-blue-green-deployments-with-kubernetes-and-istio/)
