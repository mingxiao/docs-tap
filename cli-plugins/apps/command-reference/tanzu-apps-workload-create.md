# Tanzu apps workload create

This topic helps you create a workload with the specified configuration.

### <a id="synopsis"></a> Synopsis

Create a workload with the specified configuration.

Workload configuration options include:

- Source code to build
- Runtime resource limits
- Environment variables
- Services to bind

```console
tanzu apps workload create [name] [flags]
```

## <a id="examples"></a>Examples

```console
tanzu apps workload create my-workload --git-repo https://example.com/my-workload.git
tanzu apps workload create my-workload --local-path . --source-image registry.example/repository:tag
tanzu apps workload create --file workload.yaml
```

## <a id="options"></a>Options

```console
      --annotation "key=value" pair    annotation is represented as a "key=value" pair, or "key-" to remove. This flag may be specified multiple times
      --app name                       application name the workload is a part of
      --build-env "key=value" pair     build environment variables represented as a "key=value" pair, or "key-" to remove. This flag may be specified multiple times
      --debug                          put the workload in debug mode, --debug=false to disable
      --dry-run                        print kubernetes resources to stdout rather than apply them to the cluster, messages normally on stdout will be sent to stderr
      --env "key=value" pair           environment variables represented as a "key=value" pair, or "key-" to remove. This flag may be specified multiple times
  -f, --file file path                 file path containing the description of a single workload, other flags are layered on top of this resource. Use value "-" to read from stdin
      --git-branch branch              branch within the git repo to checkout
      --git-commit SHA                 commit SHA within the git repo to checkout
      --git-repo url                   git url to remote source code
      --git-tag tag                    tag within the git repo to checkout
  -h, --help                           help for create
      --image image                    pre-built image, skips the source resolution and build phases of the supply chain
      --label "key=value" pair         label is represented as a "key=value" pair, or "key-" to remove. This flag may be specified multiple times
      --limit-cpu cores                the maximum number of CPU cores allowed (500m = .5 cores)
      --limit-memory bytes             the maximum amount of memory allowed, in bytes (500Mi = 500MiB = 500 * 1024 * 1024)
      --live-update                    put the workload in live update mode, --live-update=false to disable
      --local-path path                path on the local file system to a directory of source code to build for the workload
  -n, --namespace name                 kubernetes namespace (defaulted from kube config)
      --param "key=value" pair         additional parameters represented as a "key=value" pair, or "key-" to remove. This flag may be specified multiple times
      --request-cpu cores              the minimum amount of cpu required, in CPU cores (500m = .5 cores)
      --request-memory bytes           the minimum amount of memory required, in bytes (500Mi = 500MiB = 500 * 1024 * 1024)
      --service-ref object reference   object reference for a service to bind to the workload "database=rabbitmq.com/v1beta1:RabbitmqCluster:[my-broker-ns]:my-broker", or "database-" to delete. This flag may be specified multiple times.
      --source-image image             destination image repository where source code is staged before being built
      --tail                           show logs while waiting for workload to become ready
      --tail-timestamp                 show logs and add timestamp to each log line while waiting for workload to become ready
      --type type                      distinguish workload type
      --wait                           waits for workload to become ready
      --wait-timeout duration          timeout for workload to become ready when waiting (default 10m0s)
  -y, --yes                            accept all prompts
```

## <a id="parent-commands-options"></a> Options inherited from parent commands

```console
      --context name      name of the kubeconfig context to use (default is current-context defined by kubeconfig)
      --kubeconfig file   kubeconfig file (default is $HOME/.kube/config)
      --no-color          disable color output in terminals
  -v, --verbose int32     number for the log level verbosity (default 1)
```

## <a id="see-also"></a> See also

- [Tanzu Apps Workload](tanzu-apps-workload.md) - Workload life cycle management
