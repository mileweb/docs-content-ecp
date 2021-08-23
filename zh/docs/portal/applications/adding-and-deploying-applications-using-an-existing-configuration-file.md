# Adding and Deploying Applications Using an Existing Configuration File

1. [Configure an application](</docs/portal/applications/configuring-applications.md>) outside of the portal.
3. In the left pane of the portal, click **Applications**.
4. At the top right of the Applications page, click the **\+ Add New Application** button. 

<p align=center><img src="/docs/resources/images/applications/applications.png" width="600"></p>

4. When prompted, click **Use a YAML/JSON file**.

<p align=center><img src="/docs/resources/images/applications/applications-add.png" width="600"></p>

5. In the **Application Name** field, enter a name that helps you identify this application.
6. In the **Application Specification** field, upload the local YAML or JSON file, enter a URL that points to the file, or drag and drop the file into the designated location on the form.

<p align=center><img src="/docs/resources/images/applications/applications-add-upload-spec.png" width="600"></p>

7. Click **Submit & Deploy**.<br>

**Note:** The application deployment process may take up to a few minutes, depending on the size of container images to be pulled, the target locations, and the number of expected instances. Once the application is deployed, **Deployed** appears as its status on the Applications page. To check the status and other details, use the applications list view and detail view. After the application is deployed, you can retrieve instances in [list view](</docs/portal/applications/retrieving-instances-of-an-application.md#retrieving-instances-of-an-application-in-list-view>) or [map view](</docs/portal/applications/retrieving-instances-of-an-application.md#retrieving-instances-of-an-application-in-map-view>). If you encounter a problem, [troubleshoot the application](</docs/portal/applications/troubleshooting-an-application.md>).
