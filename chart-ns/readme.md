To test what will be applied:
```
helm template test ./chart-ns/ -f <path to values file>
```
To apply to a cluster:
```
helm upgrade --install <namespace>-ns ./chart-ns/ -f <path to values file>
```