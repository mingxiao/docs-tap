# Overview

Tanzu Application Platform v1.2 includes:

- Five new default roles to help you set up permissions for users and [service accounts](https://kubernetes.io/docs/tasks/configure-pod-container/configure-service-account/) within a namespace on a cluster that runs one of the Tanzu Application Platform profiles.
- A Tanzu CLI RBAC (role-based access control) plug-in for role binding. For more information, see [Bind a user or group to a default role](binding.md).
- Documentation for [integrating with your existing identity management solution](integrating-identity.md).

## <a id="default-roles"></a> Default roles

Three roles are for users:

- app-editor
- app-viewer
- app-operator

Two roles are for service accounts associated with the Tanzu Supply Chain:

- workload
- deliverable

The default roles provide an opinionated starting point for the most common permissions that users
need when using Tanzu Application Platform.
However, as described in the [Kubernetes documentation](https://kubernetes.io/docs/reference/access-authn-authz/rbac/)
about RBAC, you can create customized roles and permissions that better meet your needs.
Aggregated cluster roles are used to build VMware Tanzu Application Platform default roles.

The default roles are installed with every Tanzu Application Platform profile.
For an overview of the different roles and their permissions, see [Role Descriptions](role-descriptions.md).

## <a id="work-with-roles"></a> Working with roles using the RBAC CLI plug-in

For more information about working with roles, see [Bind a user or group to a default role](binding.md).

## <a id="disclaimer"></a> Disclaimer

[Tanzu Application Platform GUI](../tap-gui/about.md) does not make use of the described roles.
Instead, it provides the user with view access for each cluster.
