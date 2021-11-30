# Adding and Deploying Applications Using an Existing Configuration File

1. [Configure an application](</docs/portal/applications/configuring-applications.md>) outside of the portal.
3. In the left pane of the portal, click **Applications**.
4. At the top right of the Applications page, click the **\+ Add New Application** button. 

<p align=center><img src="/docs/resources/images/applications/applications.png" width="600"></p>

4. When prompted, click **Use a YAML/JSON file**.

<p align=center><img src="/docs/resources/images/applications/applications-add.png" width="600"></p>

5. In the **Application Name** field, enter a name that helps you identify this application.
6. In the **Application Specification** field, upload a local YAML or JSON file, or enter a URL that points to a remote file.

<p align=center><img src="/docs/resources/images/applications/applications-add-upload-spec.png" width="600"></p>

7. Click **Submit & Deploy**.<br>

**Note:** The application deployment process will take a while, the length depending on the size of container images to be downloaded, the target locations, and the number of expected instances, etc. Once the application is deployed, **Deployed** appears as its status on the Applications page. To check the status and other details, use the applications list view and detail view. After the application is deployed, you can [check application instances](</docs/portal/applications/retrieving-instances-of-an-application.md>). If you encounter a problem, [try to troubleshoot](</docs/portal/applications/troubleshooting-an-application.md>).
