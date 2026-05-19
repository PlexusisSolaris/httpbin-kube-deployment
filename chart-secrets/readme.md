To test what will be applied:
```
helm template test ./chart-secrets/ -f ./chart-secrets/values-<app name>.yaml
```
To apply to a cluster:
```
helm upgrade --install <app name>-secrets ./chart-secrets/ -f ./chart-secrets/values-<app name>.yaml
```