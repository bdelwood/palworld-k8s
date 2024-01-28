# palworld-k8s

A Helm chart to deploy a Palworld dedicated server. This chart relies on the [`thijsvanloef/palworld-server-docker`](https://github.com/thijsvanloef/palworld-server-docker) image.

# How to use

```bash
helm repo add palworld-k8s https://bdelwood.github.io/palworld-k8s/
helm repo update
helm install palworld-server palworld-k8s/palworld-k8s  \
  --set gameServer.serverName=palworld-example \
  --set password=changeme \
```

By default, the server is not configured as a community server, and RCON is enabled.

The chart will generate default server and admin (RCON) passwords, which can be retrieved with

```bash
kubectl get secrets <secrets-name> -o json | jq '.data | map_values(@base64d)'
```

Alternatively, the password can be supplied in the `values` file or by specifying existing secrets. These secrets must have the `admin-password` and `server-password` keys.

By default, the chart will provision a PVC using the default StorageClass. You can also provide an existing PVC, or change the StorageClass.

# Configuration

Full configuration options are detailed in the [Chart readme](/chart/palworld-k8s/README.md).

# Roadmap

- [ ] Implement health check/readiness check
- [ ] Support editing server settings
