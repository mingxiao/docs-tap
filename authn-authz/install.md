# Install default roles independently

This document describes how to install default roles for Tanzu Application Platform without deploying a Tanzu Application Platform profile.

>**Note:** Use the instructions on this page if you do not want to use a profile to install packages.
The full profile includes the defaults roles package.
For more information about profiles, see [About Tanzu Application Platform package and profiles](../about-package-profiles.md).

## <a id='prereqs'></a>Prerequisites

Before installing default roles, complete all prerequisites to install Tanzu Application Platform. For more information, see [Prerequisites](../prerequisites.md).

## <a id='install'></a>Install

To install default roles:

1. List version information for the package by running:

    ```console
    tanzu package available list tap-auth.tanzu.vmware.com --namespace tap-install
    ```

    For example:

    ```console
    $ tanzu package available list tap-auth.tanzu.vmware.com --namespace tap-install
    - Retrieving package versions for tap-auth.tanzu.vmware.com...
      NAME                         VERSION       RELEASED-AT
      tap-auth.tanzu.vmware.com    1.0.1
    ```

1. Install the package by running:

    ```console
    tanzu package install tap-auth \
      --package-name tap-auth.tanzu.vmware.com \
      --version VERSION \
      --namespace tap-install
    ```

    Where:

    - `VERSION` is the package version number. For example, `1.0.1`.

    For example:

    ```console
    $ tanzu package install tap-auth \
      --package-name tap-auth.tanzu.vmware.com \
      --version 1.0.1 \
      --namespace tap-install
    ```
