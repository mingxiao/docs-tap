# View Runtime Resources on Authorization-Enabled Clusters in Tanzu Application Platform GUI

To visualize runtime resources on authorization-enabled clusters in Tanzu Application Platform GUI,
proceed to the software catalog component of choice and click the **Runtime Resources** tab on
the top of ribbon.

![Screenshot of Runtime Resources](../images/tap-gui-multiple-clusters.png)

After you click **Runtime Resources**, Tanzu Application Platform GUI uses your credentials to
query the clusters for the respective runtime resources.
The system verifies that you are authenticated with the OIDC providers configured for the remote
clusters.
If you are not authenticated, the system prompts you for your OIDC credentials.

Remote clusters that are not restricted by authorization are visible by using the general Service
Account of Tanzu Application Platform GUI. It is not restricted for users.
For more information about how to set up unrestricted remote cluster visibility, see
[Viewing resources on multiple clusters in Tanzu Application Platform GUI](../cluster-view-setup.html).

The type of query to the remote cluster depends on the definition of the software catalog component.
In Tanzu Application Platform GUI, there are two types of components:

    - [Globally-scoped components](#globally-scoped-components)
    - [Namespace-scoped components](#namespace-scoped-components)

This property of the component affects runtime resource visibility, depending on your permissions on
a specific cluster.

If your permissions on the authorization-enabled cluster are limited to specific namespaces, you
do not have visibility into runtime resources of globally-scoped components.

You need cluster-scoped access to have visibility into runtime resources of globally-scoped
components.


## <a id="globally-scoped-comps"></a> Globally-scoped components

For globally-scoped components, when you access **Runtime Resources** Tanzu Application Platform GUI
queries all Kubernetes namespaces for runtime resources that have a matching `kubernetes-label-selector`,
usually with a `part-Of` prefix.

For example, `demo-component-a` does not have a `backstage.io/kubernetes-namespace` in the `metadata.annotations`
section. This makes it a globally-scoped component. See the following example YAML.

```yaml
apiVersion: backstage.io/v1alpha1
kind: Component
metadata:
  name: demo-component-a
  description: Demo Component A
  tags:
    - java
  annotations:
    'backstage.io/kubernetes-label-selector': 'app.kubernetes.io/part-of=component-a'
spec:
  type: service
  lifecycle: experimental
  owner: team-a
```


## <a id="namespace-scoped-comps"></a> Namespace-scoped components

If a component is namespace-scoped, when you access **Runtime Resources** Tanzu Application Platform GUI
queries only the associated Kubernetes namespace for each remote cluster that is visible to
Tanzu Application Platform GUI.

To make a component namespace-scoped, pass the following annotation to the definition
YAML file of the component:

```yaml
annotations:
  'backstage.io/kubernetes-namespace': NAMESPACE-NAME
```

Where `NAMESPACE-NAME` is the Kubernetes namespace you want to associate your component with.

For example, `demo-component-b` has a `kubernetes-namespace` in the `metadata.annotations` section,
which associates it with the `component-b` namespaces on each of the visible clusters.
This makes it a namespace-scoped component. See the following example YAML.

```yaml
apiVersion: backstage.io/v1alpha1
kind: Component
metadata:
  name: demo-component-b
  description: Demo Component B
  tags:
    - java
  annotations:
    'backstage.io/kubernetes-label-selector': 'app.kubernetes.io/part-of=component-b'
    'backstage.io/kubernetes-namespace': component-b
spec:
  type: service
  lifecycle: experimental
  owner: team-b
```

When the `kubernetes-namespace` annotation is absent, the component is considered globally-scoped by
default. For more information, see
[Adding Namespace Annotation](https://backstage.io/docs/features/kubernetes/configuration#adding-the-namespace-annotation)
in the Backstage documentation.
