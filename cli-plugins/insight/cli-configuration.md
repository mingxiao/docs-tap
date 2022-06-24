# Configure the Tanzu Insight CLI plug-in

This topic explains how to configure the Tanzu Insight plug-in.

> **Note:** All [required setup](cli-overview.md) must be completed in addition to configuring the CLI.


## <a id='set-tar-cert'></a>Set the target and certificate authority certificate

Set the target endpoint and CA certificate by running:

```console
tanzu insight config set-target https://metadata-store-app.metadata-store.svc.cluster.local:PORT --ca-cert PATH
```
Where

- `PORT` is the target endpoint port
- `PATH` is the direct path to the CA certificate

For example:

```console
$ tanzu insight config set-target https://metadata-store-app.metadata-store.svc.cluster.local:8443 --ca-cert /tmp/ca.crt

ℹ  Using config file: /Users/username/.config/tanzu/insight/config.yaml
ℹ  Setting trustedcacert in config
ℹ  Setting endpoint in config to: https://metadata-store-app.metadata-store.svc.cluster.local:8443
✔  Success: Set Metadata Store endpoint
```

## <a id='check-con'></a>Check the connection

Check that your configuration is correct and you are able to make a connection.

```console
tanzu insight health
```

For example:

```console
$ tanzu insight health
Success: Reached Metadata Store!
```
