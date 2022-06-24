# Accelerator custom resource definition

The `Accelerator` custom resource definition (CRD) defines any accelerator resources to be made available to the Application Accelerator for VMware Tanzu system. It is a namespaced CRD, meaning that any resources created belong to a namespace. In order for the resource to be available to the Application Accelerator system, it must be created in the namespace that the Application Accelerator UI server is configured to watch.

The `Fragment` custom resource definition (CRD) defines any accelerator fragment resources to be made available to the Application Accelerator for VMware Tanzu system. It is a namespaced CRD, meaning that any resources created belong to a namespace. In order for the resource to be available to the Application Accelerator system, it must be created in the namespace that the Application Accelerator UI server is configured to watch.

## <a id="api-definitions"></a>API definitions

The `Accelerator` CRD is defined with the following properties:

| Property | Value |
| --- | --- |
| Name | Accelerator |
| Group | accelerator.apps.tanzu.vmware.com |
| Version | v1alpha1 |
| ShortName | acc |

The `Accelerator` CRD _spec_ defined in the `AcceleratorSpec` type has the following fields:

| Field | Description | Required/Optional |
| --- | --- | --- |
| displayName | A short descriptive name used for an Accelerator. | Optional (*) |
| description | A longer description of an Accelerator. | Optional (*) |
| iconUrl | A URL for an image to represent the Accelerator in a UI. | Optional (*) |
| tags | An array of strings defining attributes of the Accelerator that can be used in a search. | Optional (*) |
| git | Defines the accelerator source Git repository. | Optional (***) |
| git.url | The repository URL, can be a HTTP/S or SSH address. | Optional (***) |
| git.ignore | Overrides the set of excluded patterns in the .sourceignore format (which is the same as .gitignore). If not provided, a default of `.git/` is used. | Optional (**) |
| git.interval | The interval at which to check for repository updates. If not provided it defaults to 10 min. There is an additional refresh interval (currently 10s) involved before accelerators may appear in the UI. There could be a 10s delay before changes are reflected in the UI.*| Optional (**) |
| git.ref | Git reference to checkout and monitor for changes, defaults to master branch. | Optional (**) |
| git.ref.branch | The Git branch to checkout, defaults to master. | Optional (**) |
| git.ref.commit | The Git commit SHA to checkout, if specified tag filters are ignored. | Optional (**) |
| git.ref.semver | The Git tag semver expression, takes precedence over tag. | Optional (**) |
| git.ref.tag | The Git tag to checkout, takes precedence over branch. | Optional (**) |
| git.secretRef | The secret name containing the Git credentials. For HTTPS repositories, the secret must contain user name and password fields. For SSH repositories, the secret must contain identity, identity.pub, and known_hosts fields. | Optional (**) |
| source | Defines the source image repository. | Optional (***) |
| source.image | Image is a reference to an image in a remote registry. | Optional (***) |
| source.imagePullSecrets | ImagePullSecrets contains the names of the Kubernetes Secrets containing registry login information to resolve image metadata. | Optional |
| source.interval | The interval at which to check for repository updates. | Optional |
| source.serviceAccountName | ServiceAccountName is the name of the Kubernetes ServiceAccount used to authenticate the image pull if the service account has attached pull secrets. | Optional |

The `Fragment` CRD is defined with the following properties:

| Property | Value |
| --- | --- |
| Name | Fragment |
| Group | accelerator.apps.tanzu.vmware.com |
| Version | v1alpha1 |
| ShortName | frag |

The `Fragment` CRD _spec_ defined in the `FragmentSpec` type has the following fields:

| Field | Description | Required/Optional |
| --- | --- | --- |
| displayName | DisplayName is a short descriptive name used for a Fragment. | Optional |
| git | Defines the fragment source Git repository. | Required |
| git.url | The repository URL, can be a HTTP/S or SSH address. | Required |
| git.ignore | Overrides the set of excluded patterns in the .sourceignore format (which is the same as .gitignore). If not provided, a default of `.git/` is used. | Optional (**) |
| git.interval | The interval at which to check for repository updates. If not provided it defaults to 10 min.| Optional (**) |
| git.ref | Git reference to checkout and monitor for changes, defaults to master branch. | Optional (**) |
| git.ref.branch | The Git branch to checkout, defaults to master. | Optional (**) |
| git.ref.commit | The Git commit SHA to checkout, if specified tag filters are ignored. | Optional (**) |
| git.ref.semver | The Git tag semver expression, takes precedence over tag. | Optional (**) |
| git.ref.tag | The Git tag to checkout, takes precedence over branch. | Optional (**) |
| git.secretRef | The secret name containing the Git credentials. For HTTPS repositories, the secret must contain user name and password fields. For SSH repositories, the secret must contain identity, identity.pub, and known_hosts fields. | Optional (**) |

\* Any optional fields marked with an asterisk (*) are populated from a field of the same name in the `accelerator` definition in the `accelerator.yaml` file if that is present in the Git repository for the accelerator.

\*\* Any fields marked with a double asterisk (**) are part of the Flux GitRepository CRD that is documented in the Flux Source Controller [Git Repositories](https://fluxcd.io/docs/components/source/gitrepositories/) documentation.

\*\*\* Any fields marked with a triple asterisk (***) are optional but either `git` or `source` is required to specify the repository to use. If `git` is specified, the `git.url` is required, and if `source` is specified, `source.image` is required.

## <a id="excluding-files"></a>Excluding files

The `git.ignore` field defaults to `.git/`, which is different from the defaults provided by the Flux Source Controller GitRepository implementation. You can override this, and provide your own exclusions. For more information, see  [fluxcd/source-controller Excluding files](https://fluxcd.io/docs/components/source/gitrepositories/#excluding-files).

## <a id="non-public-repos"></a>Non-public repositories

For Git repositories that aren't accessible anonymously, you need to provide credentials in a Secret. 

- For HTTPS repositories the secret must contain user name and password fields. The password field can contain a personal access token instead of an actual password. See [fluxcd/source-controller Basic access authentication](https://fluxcd.io/docs/components/source/gitrepositories/#basic-access-authentication)
- For HTTPS with self-signed certificates, you can add a `.data.caFile value to the secret created for HTTPS authentication. See [fluxcd/source-controller HTTPS Certificate Authority](https://fluxcd.io/docs/components/source/gitrepositories/#https-certificate-authority)
- For SSH repositories, the secret must contain identity, identity.pub and known_hosts fields. See [fluxcd/source-controller SSH authentication](https://fluxcd.io/docs/components/source/gitrepositories/#ssh-authentication).

For Image repositories that aren't publicly available, an image pull secret can be provided. For more information, see [Using imagePullSecrets](https://kubernetes.io/docs/concepts/configuration/secret/#using-imagepullsecrets).

## <a id="examples"></a>Examples

A minimal example could look like the following manifest:

> hello-fun.yaml

```yaml
apiVersion: accelerator.apps.tanzu.vmware.com/v1alpha1
kind: Accelerator
metadata:
  name: hello-fun
spec:
  git:
    url: https://github.com/sample-accelerators/hello-fun
    ref:
      branch: main
```

This minimal example creates an accelerator named `hello-fun`. The `displayName`, `description`, `iconUrl`, and `tags` fields are populated based on the content under the `accelerator` key in the `accelerator.yaml` file found in the `main` branch of the Git repository at https://github.com/sample-accelerators/hello-fun. For example:

> accelerator.yaml

```yaml
accelerator:
  displayName: Hello Fun
  description: A simple Spring Cloud Function serverless app
  iconUrl: https://raw.githubusercontent.com/simple-starters/icons/master/icon-cloud.png
  tags:
  - java
  - spring
  - cloud
  - function
  - serverless

...
```

We can also explicitly specify the `displayName`, `description`, `iconUrl`, and `tags` fields and this overrides any values provided in the accelerator's Git repository. The following example explicitly sets those fields plus the `ignore` field:

> my-hello-fun.yaml

```yaml
apiVersion: accelerator.apps.tanzu.vmware.com/v1alpha1
kind: Accelerator
metadata:
  name: my-hello-fun
spec:
  displayName: My Hello Fun
  description: My own Spring Cloud Function serverless app
  iconUrl: https://github.com/simple-starters/icons/raw/master/icon-cloud.png
  tags:
    - spring
    - cloud
    - function
    - serverless
  git:
    ignore: ".git/, bin/"
    url: https://github.com/sample-accelerators/hello-fun
    ref:
      branch: test
```

## <a id="git-repo-example"></a>Example for a private Git repo

To create an accelerator by using a private Git repository, first create a secret by using HTTP credentials or SSH credentials.

### <a id="http-cred-example"></a>Example using http credentials

>**Note:** For better security, use an access token as the password.

```shell
kubectl create secret generic https-credentials \
    --from-literal=username=<user> \
    --from-literal=password=<password>
```

> https-credentials.yaml

```yaml
apiVersion: v1
kind: Secret
metadata:
  name: https-credentials
  namespace: default
type: Opaque
data:
  username: <BASE64>
  password: <BASE64>
```

After you have the secret file, you can create the accelerator by using the `secretRef` property:

> private-acc.yaml

```yaml
apiVersion: accelerator.apps.tanzu.vmware.com/v1alpha1
kind: Accelerator
metadata:
  name: private-acc
spec:
  displayName: private
  description: Accelerator using private repository
  git:
    url: <repository-URL>
    ref:
      branch: main
    secretRef:
      name: https-credentials
```

### <a id="ssh-example"></a>Example using SSH credentials

```shell
ssh-keygen -q -N "" -f ./identity
ssh-keyscan github.com > ./known_hosts
kubectl create secret generic ssh-credentials \
    --from-file=./identity \
    --from-file=./identity.pub \
    --from-file=./known_hosts
```

This example assumes you don't have a key file already created. If you do, replace the values using the following format:  

`--from-file=identity=<path to your identity file>`

`--from-file=identity.pub=<path to your identity.pub file>`

`--from-file=known_hosts=<path to your know_hosts file>`

> ssh-credentials.yaml

```yaml
apiVersion: v1
kind: Secret
metadata:
  name: ssh-credentials
  namespace: default
type: Opaque
data:
  identity: <BASE64>
  identity.pub: <BASE64>
  known_hosts: <BASE64>
```

> private-acc-ssh.yaml

```yaml
apiVersion: accelerator.apps.tanzu.vmware.com/v1alpha1
kind: Accelerator
metadata:
  name: private-acc
spec:
  displayName: private
  description: Accelerator using private repository
  git:
    url: <repository-URL>
    ref:
      branch: main
    secretRef:
      name: ssh-credentials
```
