# Application Accelerator in Tanzu Application Platform GUI

This topic describes Application Accelerator in Tanzu Application Platform GUI.


## <a id="overview"></a> Overview

Application Accelerator for VMware Tanzu helps you bootstrap developing and deploying your
applications in a discoverable and repeatable way.

Enterprise Architects author and publish accelerator projects that provide developers and operators
with ready-made, enterprise-conformant code and configurations.
You can then use Application Accelerator to create new projects based on those accelerator projects.

The Application Accelerator user interface (UI) enables you to discover available accelerators,
configure them, and generate new projects to download.


## <a id='entry-point'></a>Entry point to Application Accelerator

The Application Accelerator UI plug-in is part of Tanzu Application Platform GUI.
To access Application Accelerator, click **Create** in the left-hand navigation bar of
Tanzu Application Platform. This opens the **Accelerators** page.

![Screenshot of Accelerators page](images/aa1-acc-page.png)

Here you can view accelerators already registered with the system.
Developers can add new accelerators by registering them with Kubernetes.

Every accelerator provides a title and short description. You can view an accelerator definition by
clicking **View Repository**, which opens the accelerator's Git repository in a new browser tab.

This main page allows you to search and filter based on text and tags associated with the accelerators.
When you find the accelerator representing the project you want to create, click **Choose**.
This opens the **Generate Accelerators** page.


## <a id='configure-project'></a> Configuring project generation

On the **Generate Accelerators** page, supply any configuration options needed to generate the project.
The Application Architect has defined these in the `accelerator.yaml` in the accelerator definition.
Setting some options can cause others to appear that also must be specified.

![Example configuration page for an accelerator.](./images/aa2-configuringAnAccelerator.png)


## <a id='explore-project'></a> Exploring a project during configuration

Click **Explore** on the **Generate Accelerators** page to view the project before it is generated.
This opens the **Explore Project** page as shown in the following screenshot.

![Screenshot of the Explore Project page.](images/aa3-exploringProject.png)

When you've finished configuring your project, click **Next Step** to see the project summary page.
You are now ready to create the project.


## <a id='project-summary'></a>Project summary

This page shows the values you have specified for the configurable options.

![Screenshot showing the configured project summary.](images/aa4-configuredProjectSummary.png)

You can return to customize options by clicking **Back** if needed.
Otherwise, you're ready to generate your accelerator.


## <a id='create-project'></a>Creating the project

To generate your project, click **Create**.
The system starts generating your project and the Task Activity page shows the progress, with
detailed logs on the right side.

![Task activity during project creation](images/aa5-taskActivity.png)

After the project is generated, you can:

- Click **Explore Zip File**. This opens the Explore Project page to verify configuration.
- Click **Download Zip File** to download the project in a ZIP file.


## <a id='develop-your-code'></a>Develop your code

After you've downloaded the ZIP file, expand it, and open the project in your integrated development
environment (IDE).

![Screenshot of working on a project in Visual Studio Code](images/aa6-ide.png)


## <a id='next-steps'></a>Next steps

To learn more about Application Accelerator for VMware Tanzu, see the
[Application Accelerator documentation](https://docs.vmware.com/en/Application-Accelerator-for-VMware-Tanzu/index.html).
