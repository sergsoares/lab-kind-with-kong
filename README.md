# Lab - Kind Cluster with Kong Ingress

## Dependencies

- [Kind v0.12.0](https://kind.sigs.k8s.io/docs/user/quick-start/)
- [Kubectl 1.22](https://kubernetes.io/docs/tasks/tools/install-kubectl/)

## Structure

```
$ tree
.
├── README.md
├── scripts
│   ├── create-cluster
│   ├── info
│   ├── kong-install
│   ├── setup
│   ├── setup-delete
│   └── simple-pod-install
└── src
    └── kind-config
        └── clusterconfig.yml

3 directories, 8 files
```

## Creating cluster with kind (supporting ingress)

Above a already create sript to install cluster with prepared informations

```
$ bash scripts/setup
Creating cluster "kind-lab" ...
 ✓ Ensuring node image (kindest/node:v1.23.4) 🖼
 ✓ Preparing nodes 📦  
 ✓ Writing configuration 📜 
 ✓ Starting control-plane 🕹️ 
 ✓ Installing CNI 🔌 
 ✓ Installing StorageClass 💾 
Set kubectl context to "kind-kind-lab"
You can now use your cluster with:

kubectl cluster-info --context kind-kind-lab

Not sure what to do next? 😅  Check out https://kind.sigs.k8s.io/docs/user/quick-start/
Kubernetes control plane is running at https://127.0.0.1:37655
CoreDNS is running at https://127.0.0.1:37655/api/v1/namespaces/kube-system/services/kube-dns:dns/proxy

To further debug and diagnose cluster problems, use 'kubectl cluster-info dump'.
namespace/kong created
customresourcedefinition.apiextensions.k8s.io/kongclusterplugins.configuration.konghq.com created
customresourcedefinition.apiextensions.k8s.io/kongconsumers.configuration.konghq.com created
customresourcedefinition.apiextensions.k8s.io/kongingresses.configuration.konghq.com created
customresourcedefinition.apiextensions.k8s.io/kongplugins.configuration.konghq.com created
customresourcedefinition.apiextensions.k8s.io/tcpingresses.configuration.konghq.com created
customresourcedefinition.apiextensions.k8s.io/udpingresses.configuration.konghq.com created
serviceaccount/kong-serviceaccount created
role.rbac.authorization.k8s.io/kong-leader-election created
clusterrole.rbac.authorization.k8s.io/kong-ingress created
rolebinding.rbac.authorization.k8s.io/kong-leader-election created
clusterrolebinding.rbac.authorization.k8s.io/kong-ingress created
service/kong-proxy created
service/kong-validation-webhook created
deployment.apps/ingress-kong created
ingressclass.networking.k8s.io/kong created
deployment.apps/ingress-kong patched
pod/foo-app created
service/foo-service created
pod/bar-app created
service/bar-service created
ingress.networking.k8s.io/example-ingress created
ingress.networking.k8s.io/example-ingress patched
```

After that you can run commands to validate cluster

```
$ curl localhost/foo
foo
$ curl localhost/bar
bar
```