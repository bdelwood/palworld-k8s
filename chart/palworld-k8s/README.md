# palworld-k8s

![Version: 0.11.0](https://img.shields.io/badge/Version-0.11.0-informational?style=flat-square) ![Type: application](https://img.shields.io/badge/Type-application-informational?style=flat-square) ![AppVersion: v0.39.3](https://img.shields.io/badge/AppVersion-v0.39.3-informational?style=flat-square)

A basic chart to deploy Palworld dedicated servers.

## Source Code

* <https://github.com/bdelwood/palworld-k8s>

## Requirements

Kubernetes: `>=1.26.0-0`

## Values

| Key | Type | Default | Description |
|-----|------|---------|-------------|
| affinity | object | `{}` | Affinity rules for pod scheduling. |
| extraEnv | object | `{}` | Define extra environment variables to pass directly to the container. Any env vars which are set by other values will be overridden. Useful for defining the env vars for setting up Discord webhooks. |
| fullnameOverride | string | `""` | Override the full name of the chart. Default is a combination of release name and chart name. |
| gameServer.auto_reboot.check_if_players_online | bool | `false` | Check if players are online before auto rebooting. |
| gameServer.auto_reboot.cron_expression | string | `"0 0 * * *"` | Cron expression for automatic reboots. Defines when to reboot. The default value schedules a reboot  at midnight every day. Use standard cron format. |
| gameServer.auto_reboot.enabled | bool | `false` | Enable or disable automatic pod reboots. This feature is to alleviate some issues seen with memory leaks. |
| gameServer.auto_reboot.warn_minutes | int | `5` | Time, in minutes, to send a server message to warn users before a reboot.  |
| gameServer.auto_update.cron_expression | string | `"0 * * * *"` | Cron expression for updates. Defines when the update check should run. The default value checks for updates every hour. Use standard cron format. |
| gameServer.auto_update.enabled | bool | `false` | Enable or disable automatic updates. |
| gameServer.auto_update.warn_minutes | int | `30` | Time, in minutes, to send a server message to warn users before an update.  |
| gameServer.backup.cron_expression | string | `"0 0 * * *"` | Cron expression for backup scheduling. Defines when the backups should be triggered. The default value schedules a backup at midnight every day. Use standard cron format. |
| gameServer.backup.delete_old_backups | bool | `false` | Flag to decide whether to delete old backups. If set to true, backups older than a specified number of days will be deleted. |
| gameServer.backup.enabled | bool | `true` | Enable or disable automatic backups. |
| gameServer.backup.old_backup_days | int | `30` | The number of days to keep old backups. If `delete_old_backups` is enabled, backups older than this number of days will be deleted. |
| gameServer.community.enabled | bool | `false` | Enable if you want your server to show up as a community server. |
| gameServer.community.service.nodePort | int | `nil` | Node port a community server (for NodePort service type). |
| gameServer.community.service.port | int | `27015` | Service port for a community server. |
| gameServer.disable_generate_engine | bool | `false` | Whether to generate Engine.ini from environment variables (passed from values). |
| gameServer.disable_generate_settings | bool | `false` | Whether to generate PalWorldSettings.ini from environment variables (passed from values). |
| gameServer.existingSecret | string | `""` | Name of an existing secret for the server password. |
| gameServer.install_beta_insider | bool | `false` | Install the beta Palworld dedicated server. |
| gameServer.multithreading | bool | `true` | Enable multithreading. |
| gameServer.password | string | `""` | Server password If one is not provided or an existing secret it not provided, one will be generated. |
| gameServer.platform | string | `"steam"` | Configure the server for Steam or Xbox players. |
| gameServer.player_logging.enabled | bool | `true` | Whether to announce and log when players join or leave |
| gameServer.player_logging.poll_period | int | `5` | Time, in seconds, to poll for player changes  |
| gameServer.players | int | `16` | Number of players allowed on the server concurrently. |
| gameServer.rest_api.enabled | bool | `false` | Whether to enable the [REST API](https://tech.palworldgame.com/api/rest-api/palwold-rest-api/). DO NOT EXPOSE TO THE PUBLIC INTERNET.  |
| gameServer.rest_api.port | int | `8212` |  |
| gameServer.serverDescription | string | `""` | Description for the server. |
| gameServer.serverName | string | `""` | Custom server name. |
| gameServer.service.nodePort | int | `nil` | Node port for the game server (for NodePort service type). |
| gameServer.service.port | int | `8211` | Service port for the game server. |
| gameServer.target_manifest_id | string | `nil` | Locks game version to specific manifest ID from Steam Download Depot. |
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
| probes | object | `{"liveness":{},"readiness":{}}` | Liveness and readiness probes. |
| probes.liveness | object | `{}` | Liveness probe |
| probes.readiness | object | `{}` | Readiness probe. |
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
