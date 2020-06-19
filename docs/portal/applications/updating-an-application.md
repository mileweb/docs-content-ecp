# Updating an Application

The following procedure describes how to update applications from the Applications page. You can also update applications from the form used to [view application information](</docs/portal/applications/viewing-application-information.md>).

1. In the left pane, click **Applications**.
2. Find the application you want to update, then click its **Actions** menu and select **Update**. An Update Application form similar to the following appears.

![null](</docs/resources/images/applications/applications-update.png>)

3. Complete the fields in the Update Application form. Required fields are denoted by an asterisk (\*).

| **Fields**                                                                                                                                             | **Description**                                                                                                                                        |
| ------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------ |
| Application Name                                                                                                                                       | Read-only field that shows the name of the application.                                                                                                |
| HTTP Method                                                                                                                                            | Select the HTTP method to be used with update operations. Choices are:<br><ul><li><strong>Patch</strong> = patch requests are used to make changes to part of the resource at a location. This selection patches the resource, changing its properties. It is used to make minor updates to resources. </li><li><strong>Put</strong></strong> = puts resources at a location. Put requests always contain a full resource.</li>                                                                                  |
| Application Specification                                                                                                                              | Select a local YAML or JSON file, enter a URL where the YAML or JSON file is located, or drag and drop the file to the location indicated in the form. |

4. Click **Submit & Deploy** to update your application automatically across ECP edge locations.<br>

    **Note:** Observe the following behaviors:

    - The application deployment process may take up to a few minutes, depending on the size of container images to be pulled, the target locations, and the number of expected instances. Once the application is deployed, **Deployed** appears as its status on the Applications page. To check the status and other details, use the applications list view and detail view. After the application is deployed, you can retrieve instances in [list view](</docs/portal/applications/retrieving-instances-of-an-application.md#retrieving-instances-of-an-application-in-list-view>) or [map view](</docs/portal/applications/retrieving-instances-of-an-application.md#retrieving-instances-of-an-application-in-map-view>).
    - Updating an application using the method PUT replaces all existing objects, including any persistent storage volumes, of the application.
    - Scaling down or redistributing an application that uses persistent storage volumes might delete existing persistent volumes along with pod instances.