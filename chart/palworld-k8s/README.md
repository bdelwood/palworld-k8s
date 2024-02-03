# palworld-k8s

![Version: 0.3.0](https://img.shields.io/badge/Version-0.3.0-informational?style=flat-square) ![Type: application](https://img.shields.io/badge/Type-application-informational?style=flat-square) ![AppVersion: v0.21.0](https://img.shields.io/badge/AppVersion-v0.21.0-informational?style=flat-square)

A basic chart to deploy Palworld dedicated servers.

## Source Code

* <https://github.com/bdelwood/palworld-k8s>

## Requirements

Kubernetes: `>=1.26.0-0`

## Values

| Key | Type | Default | Description |
|-----|------|---------|-------------|
| affinity | object | `{}` | Affinity rules for pod scheduling. |
| fullnameOverride | string | `""` | Override the full name of the chart. Default is a combination of release name and chart name. |
| gameServer.auto_reboot.cron_expression | string | `"0 0 * * *"` |  |
| gameServer.auto_reboot.enabled | bool | `false` |  |
| gameServer.auto_reboot.warn_minutes | int | `5` |  |
| gameServer.auto_update.cron_expression | string | `"0 * * * *"` |  |
| gameServer.auto_update.enabled | bool | `false` |  |
| gameServer.auto_update.warn_minutes | int | `30` |  |
| gameServer.backup.cron_expression | string | `"0 0 * * *"` | Cron expression for backup scheduling. Defines when the backups should be triggered. The default value here schedules a backup at midnight every day. Use standard cron format. |
| gameServer.backup.delete_old_backups | bool | `false` | Flag to decide whether to delete old backups. If set to true, backups older than a specified number of days will be deleted. |
| gameServer.backup.enabled | bool | `true` | Enable or disable automatic backups. |
| gameServer.backup.old_backup_days | int | `30` | The number of days to keep old backups. If `delete_old_backups` is enabled, backups older than this number of days will be deleted. |
| gameServer.community.enabled | bool | `false` | Enable if you want your server to show up as a community server. |
| gameServer.community.service.nodePort | int | `nil` | Node port a community server (for NodePort service type). |
| gameServer.community.service.port | int | `27015` | Service port for a community server. |
| gameServer.existingSecret | string | `""` | Name of an existing secret for the server password. |
| gameServer.multithreading | bool | `true` | Enable multithreading. |
| gameServer.password | string | `""` | Server password If one is not provided or an existing secret it not provided, one will be generated. |
| gameServer.players | int | `16` | Number of players allowed on the server concurrently. |
| gameServer.serverDescription | string | `""` | Description for the server. |
| gameServer.serverName | string | `""` | Custom server name. |
| gameServer.service.nodePort | int | `nil` | Node port for the game server (for NodePort service type). |
| gameServer.service.port | int | `8211` | Service port for the game server. |
| gameServer.world_parameters | object |  | Configure the game world settings. Use quotes to avoid validation issues. Accepted values are given [here](https://github.com/thijsvanloef/palworld-server-docker/blob/main/.env.example) |
| image.pullPolicy | string | `"IfNotPresent"` | Image pull policy |
| image.registry | string | `"docker.io"` | Container registry for the image. |
| image.repository | string | `"thijsvanloef/palworld-server-docker"` | Image repository |
| image.tag | string | `""` | Overrides the image tag. Default is the chart appVersion. |
| nameOverride | string | `""` | Override the name of the chart. Default is the chart name. |
| nodeSelector | object | `{}` | Node selector for pod scheduling. |
| persistence.accessMode | string | `"ReadWriteOnce"` | Access mode for the persistent volume. |
| persistence.enabled | bool | `true` | Enable or disable persistence. |
| persistence.existingClaim | string | `""` | Name of an existing persistentVolumeClaim. |
| persistence.preventDelete | bool | `true` | Prevent Helm from deleting the PVC. Some storageClasses (such as the local-path-provisioner installed by default by k3s) have reclaimPolicy: Delete. |
| persistence.size | string | `"12Gi"` | Size of the persistent volume. |
| persistence.storageClassName | string | `""` | Storage class name for the PVC. |
| podAnnotations | object | `{}` | Annotations to add to the pod. |
| podSecurityContext | object | `{}` | Security context for the pod. |
| rcon.enabled | bool | `true` | Enable or disable RCON. |
| rcon.existingSecret | string | `""` | Name of an existing secret for the RCON (admin) password. |
| rcon.password | string | `""` | RCON (admin) password. If one is not provided and RCON is enabled, one will be generated. |
| rcon.service.nodePort | int | `nil` | Node port for RCON (for NodePort service type). |
| rcon.service.port | int | `25575` | Service port for RCON. |
| resources.limits | object | `{"cpu":4,"memory":"16Gi"}` | Resource limits (CPU, Memory) for the server. |
| resources.requests | object | `{"cpu":4,"memory":"8Gi"}` | Resource requests (CPU, Memory) for the server. |
| securityContext | object | `{}` | Security context for the pod containers. |
| service.type | string | `"LoadBalancer"` | Service type (e.g., LoadBalancer, ClusterIP, NodePort) |
| serviceAccount.annotations | object | `{}` | Annotations to add to the service account. |
| serviceAccount.create | bool | `false` | Specifies whether a service account should be created. |
| serviceAccount.name | string | `""` | The name of the service account. |
| tolerations | object | `{}` | Tolerations for pod scheduling. |
| tz | string | `"UTC"` | Timezone setting for the server. |
| updateStrategy | object | `{"type":"Recreate"}` | Update strategy for deployments. |

----------------------------------------------
Autogenerated from chart metadata using [helm-docs v1.12.0](https://github.com/norwoodj/helm-docs/releases/v1.12.0)
