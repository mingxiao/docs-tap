# Customizing branding

This section describes how to customize the branding within the Tanzu Application Platform GUI portal:

* [Customize logo and portal name on the top banner](#customize-logo-name)
* [Customize Authentication page](#customize-auth-page)


## <a id="customize-logo-name"></a> Customize logo and portal name on the top banner

You can customize the logo and the name displayed in the top banner in the
Tanzu Application Platform GUI portal.  
By default, the portal displays the VMware Tanzu logo and **Tanzu Application Platform** as the name.

![Screenshot displaying the default VMware Tanzu branding within the Tanzu Application Platform GUI portal](../images/standard-branding.png)


### <a id="brand-customizing"></a> Customize branding

To customize the branding in your portal:

1. Provide additional configuration parameters to the `app_config` stanza of your `tap-values.yml` file:

    ```yaml
    tap_gui:
      app_config:
        customize:
          custom_logo: 'BASE-64-IMAGE'
          custom_name: 'PORTAL-NAME'
    ```

    Where:

    - `BASE-64-IMAGE` is the image encoded in base64. VMware recommends a 512-pixel by 512-pixel PNG image with a transparent background.
    - `PORTAL-NAME` is the name of your portal, such as `Our Custom Developer Experience Portal`.

1. Reinstall your Tanzu Application Platform GUI package by following steps in
[Upgrading Tanzu Application Platform](../../upgrading.html).

After the updated values configuration file is applied in Tanzu Application Platform GUI,
you see the customized version of your portal.

If there is an error in `BASE-64-IMAGE` or `PORTAL-NAME`, Tanzu Application Platform GUI reverts to
the original branding template.

![Screenshot displaying the custom branding within the Tanzu Application Platform GUI portal](../images/customized-branding.png)


## <a id="customize-auth-page"></a> Customize Authentication page

To customize the portal name on the **Authentication** page and the name of the browser tab
for Tanzu Application Platform GUI:

1. Provide additional configuration parameters to the `app_config` section of your `tap-values.yaml`
file:

    ```yaml
    tap_gui:
      app_config:
        app:
          title: 'CUSTOM-TAB-NAME'
    ```

    Where `CUSTOM-TAB-NAME` is the name on the Authentication page and the browser tab of your portal,
    such as `Our Organization Full Name`.

1. Reinstall your Tanzu Application Platform GUI package by following the steps in
[Upgrading Tanzu Application Platform](../../upgrading.html).

After the updated values configuration file is applied in Tanzu Application Platform GUI,
you see the customized version of your portal.
