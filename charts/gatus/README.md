# Gatus Helm Chart

> Installs the automated service health dashboard [Gatus](https://github.com/TwiN/gatus)


## Get Repo Info

```console
helm repo add twin https://twin.github.io/helm-charts
helm repo update

```console
helm delete --purge [RELEASE_NAME]
```

This removes all the Kubernetes components associated with the chart and deletes the release.
_See [helm uninstall](https://helm.sh/docs/helm/helm_uninstall/) for command documentation._


## Configuration

| Parameter                                | Description                                                                                | Default                            |
|------------------------------------------|--------------------------------------------------------------------------------------------|------------------------------------|
| `deployment.strategy`                    | Deployment strategy                                                                        | `RollingUpdate`                    |
| `deployment.annotateConfigChecksum`      | Restart pod when config changed                                                            | `true`                             |
| `readinessProbe.enabled`                 | Enable readiness probe                                                                     | `true`                             |
| `livenessProbe.enabled`                  | Enable liveness probe                                                                      | `true`                             |
| `image.repository`                       | Image repository                                                                           | `twinproduction/gatus`             |
| `image.tag`                              | Overrides the Gatus image tag                                                              | ``                                 |
| `image.sha`                              | Image sha                                                                                  | ``                                 |
| `image.pullPolicy`                       | Image pull policy                                                                          | `IfNotPresent`                     |
| `image.pullSecrets`                      | Image pull secrets                                                                         | `{}`                               |
| `hostNetwork.enabled`                    | Enable host network mode                                                                   | `false`                            |
| `annotations`                            | Deployment annotations                                                                     | `{}`                               |
| `labels`                                 | Deployment labels                                                                          | `{}`                               |
| `podAnnotations`                         | Pod annotations                                                                            | `{}`                               |
| `podLabels`                              | Pod labels                                                                                 | `{}`                               |
| `extraLabels`                            | Extra labels for all manifests                                                             | `{}`                               |
| `serviceAccount.create`                  | Create service account                                                                     | `false`                            |
| `serviceAccount.name`                    | Service account name to use                                                                | ``                                 |
| `serviceAccount.annotations`             | ServiceAccount annotations                                                                 | `{}`                               |
| `serviceAccount.autoMount`               | Automount the service account token in the pod                                             | `false`                            |
| `podSecurityContext.fsGroup`             | Pod volume's ownership GID                                                                 | `65534`                            |
| `securityContext.runAsNonRoot`           | Container runs as a non-root user                                                          | `true`                             |
| `securityContext.runAsUser`              | Container processes' UID to run the entrypoint                                             | `65534`                            |
| `securityContext.runAsGroup`             | Container processes' GID to run the entrypoint                                             | `65534`                            |
| `securityContext.readOnlyRootFilesystem` | Container's root filesystem is read-only                                                   | `true`                             |
| `service.type`                           | Type of service                                                                            | `ClusterIP`                        |
| `service.port`                           | Port for kubernetes service                                                                | `80`                               |
| `service.portName`                       | Port name for kubernetes service                                                           | `http`                             |
| `service.targetPort`                     | Port for container                                                                         | `8080`                             |
| `service.annotations`                    | Service annotations                                                                        | `{}`                               |
| `service.labels`                         | Custom labels                                                                              | `{}`                               |
| `ingress.enabled`                        | Enables Ingress                                                                            | `false`                            |
| `ingress.ingressClassName`               | Ingress ClassName (for k8s 1.18+)                                                          | ``                                 |
| `ingress.name`                           | Ingress name                                                                               | ``                                 |
| `ingress.annotations`                    | Ingress annotations (values are templated)                                                 | `{}`                               |
| `ingress.labels`                         | Custom labels                                                                              | `{}`                               |
| `ingress.path`                           | Ingress accepted path                                                                      | `/`                                |
| `ingress.pathType`                       | Ingress type of path                                                                       | `Prefix`                           |
| `ingress.extraPaths`                     | Ingress extra paths to prepend to every host                                               | `[]`                               |
| `ingress.hosts`                          | Ingress accepted hostnames                                                                 | `["chart-example.local"]`          |
| `ingress.tls`                            | Ingress TLS configuration                                                                  | `[]`                               |
| `gateway.apiVersion`                     | Gateway API Version                                                                        | `gateway.networking.k8s.io/v1`     |
| `gateway.route.enabled`                  | Enables Gateway API [HTTPRoute][gateway-api]                                               | `false`                            |
| `gateway.route.annotations`              | HTTPRoute annotations (values are templated)                                               | `{}`                               |
| `gateway.route.labels`                   | Custom labels                                                                              | `{}`                               |
| `gateway.route.path`                     | Path prefix for routing                                                                    | `/`                                |
| `gateway.route.parentRefs`               | Parent Gateway references (required)                                                       | `[]`                               |
| `gateway.route.hosts`                    | HTTPRoute accepted hostnames (values are templated)                                        | `["gatus.local"]`                  |
| `gateway.route.httpsRedirect`            | Create separate HTTPRoute for HTTP to HTTPS redirect                                       | `false`                            |
| `gateway.route.httpsRedirectParentRefs`  | Parent Gateway references for redirect route (uses parentRefs if not specified)            | `[]`                               |
| `gateway.route.additionalRules`          | Additional rules to prepend before default backend rule                                    | `[]`                               |
| `gateway.route.filters`                  | Filters to apply to the default backend rule                                               | `[]`                               |
| `env`                                    | Extra environment variables passed to pods                                                 | `{}`                               |
| `envFrom`                                | Additional envFrom configuration to use a Secret or a ConfigMap in an environment variable | `[]`                               |
| `sidecarContainers`                      | Sidecar containers in the pod                                                              | `{}`                               |
| `extraVolumeMounts`                      | Extra volume mounts                                                                        | `[]`                               |
| `secrets`                                | Include secret's content in pod environment                                                | `false`                            |
| `resources`                              | CPU/Memory resource requests/limits                                                        | `{}`                               |
| `nodeSelector`                           | Node labels for pod assignment                                                             | `{}`                               |
| `tolerations`                            | Tolerations for pod assignment                                                             | `[]`                               |
| `priorityClassName`                      | PriorityClass to be used by the gatus pod                                                  | ``                                 |
| `extraInitContainers`                    | Init containers to add to the gatus pod                                                    | `[]`                               |
| `persistence.enabled`                    | Use persistent volume to store data                                                        | `false`                            |
| `persistence.size`                       | Size of persistent volume claim                                                            | `200Mi`                            |
| `persistence.mounthPath`                 | Persistent data volume's mount path                                                        | `/data`                            |
| `persistence.subPath`                    | Mount a sub dir of the persistent volume                                                   | `nil`                              |
| `persistence.accessModes`                | Persistence access modes                                                                   | `[ReadWriteOnce]`                  |
| `persistence.finalizers`                 | PersistentVolumeClaim finalizers                                                           | `["kubernetes.io/pvc-protection"]` |
| `persistence.annotations`                | PersistentVolumeClaim annotations                                                          | `{}`                               |
| `persistence.selectorLabels`             | PersistentVolumeClaim selector labels                                                      | `{}`                               |
| `persistence.existingClaim`              | Use an existing PVC to persist data                                                        | `nil`                              |
| `persistence.storageClassName`           | Type of persistent volume claim                                                            | `nil`                              |
| `serviceMonitor.enabled`                 | Use servicemonitor from prometheus operator                                                | `false`                            |
| `serviceMonitor.namespace`               | Namespace this servicemonitor is installed in                                              | ``                                 |
| `serviceMonitor.interval`                | How frequently Prometheus should scrape                                                    | `1m`                               |
| `serviceMonitor.path`                    | Path to scrape                                                                             | `/metrics`                         |
| `serviceMonitor.scheme`                  | Scheme to use for metrics scraping                                                         | `http`                             |
| `serviceMonitor.tlsConfig`               | TLS configuration block for the endpoint                                                   | `{}`                               |
| `serviceMonitor.labels`                  | Labels for the servicemonitor object                                                       | `{}`                               |
| `serviceMonitor.scrapeTimeout`           | Timeout after which the scrape is ended                                                    | `30s`                              |
| `serviceMonitor.relabelings`             | RelabelConfigs for samples before ingestion                                                | `[]`                               |
| `networkPolicy.enabled`                  | Enable creation of NetworkPolicy resources                                                 | `false`                            |
| `networkPolicy.ingress.selectors`        | List of Ingress Rule selectors                                                             | `[]`                               |
| `config`                                 | [Gatus configuration][gatus-config]                                                        | `{}`                               |
| `externalConfigMap`                      | Name of an external ConfigMap resource. If set, `config` is ignored.                       | `""`                               |

_See [Customizing the Chart Before Installing](https://helm.sh/docs/intro/using_helm/#customizing-the-chart-before-installing)._

To see all configurable options with detailed comments, visit the chart's [values.yaml](./gatus/values.yaml), or run

```console
helm inspect values twin/gatus
```

### `helmfile.yaml` example

```yaml
---
repositories:
  - name: twin
    url: https://twin.github.io/helm-charts

releases:
  - name: gatus
    namespace: gatus
    chart: twin/gatus
    version: 1.0.0
    values:
      - persistence:
          enabled: true
      - config:
          storage:
            type: sqlite
            path: /data/data.db
          endpoints:
            - name: Example
              url: https://example.com
              conditions:
                - '[STATUS] == 200'
```


[gatus-config]: https://github.com/TwiN/gatus#configuration
[gateway-api]: https://gateway-api.sigs.k8s.io/api-types/httproute/
