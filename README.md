# helm-charts

## Adding a new chart to this repository
```sh
# Package the Helm chart and add the created .tgz file to this repository:
helm package my-chart
# Update the index.yaml file.
helm repo index helm-charts/ --url https://TwinProduction.github.io/helm-charts/
```

## Add this Helm repository
```sh
helm repo add TwinProduction https://TwinProduction.github.io/helm-charts
helm repo list
```

## Update and show charts
```sh
helm repo update
helm search repo TwinProduction
```
