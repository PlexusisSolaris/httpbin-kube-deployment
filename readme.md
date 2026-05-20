# Prerequisites
- k8s cluster ([minikube](https://minikube.sigs.k8s.io/docs/)...)
- metrics server on the cluster
    - for minikube use `minikube addons enable metrics-server`
    - [metrics-server](https://github.com/kubernetes-sigs/metrics-server)
- install [kubectl](https://kubernetes.io/docs/tasks/tools/#kubectl), [helm](https://helm.sh/docs/intro/install/)

## Namespaces and secrets
Add namespaces to [ns/values.yaml](ns/values.yaml) in `.namespaces` list. Apply then to the cluster using:
```
helm upgrade --install httpbin-dev-ns chart-ns/ -f ns/values.yaml
```
To add secrets, take a look at [secrets/values.yaml](secrets/values.yaml), copy the file and have it have suffix `*-applied.yaml`, this way, they won't be tracked by git (`.gitignore`). Apply to cluster:
```
helm upgrade --install httpbin-dev-secrets chart-secrets/ -f secrets/values-applied.yaml
```
## Deploy app
Helm chart for app deployment is in `app/` directory. To apply it:
```
helm upgrade --install httpbin-dev-app app/
```

### Templating
To template Helm charts:
```
helm template test app/
helm template test chart-ns/ -f <path to values file>
helm template test chart-secrets/ -f <path to values file>
```
### See UI
Use port forwarding to get the running app mapped to your local port:
```
kubectl port-forward svc/httpbin-svc 8080:8080 -n httpbin-dev
```