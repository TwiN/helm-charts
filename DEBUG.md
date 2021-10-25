## Debugging charts

Navigate to the folder of the chart you wish to debug and use the following command:
```console
helm install . --generate-name --dry-run --debug
```

To try installing it locally in a Kubernetes cluster:
```console
helm install . --generate-name --create-namespace --namespace helm-debug
```
