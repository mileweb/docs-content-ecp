# Updating an Application

The following procedure describes how to update applications from the Applications page. You can also update applications from the form used to [view application information](<Viewing Application Information.htm>).

1. In the left pane, click **Applications**.
2. Find the application you want to update, then click its **Actions** menu and select **Update**. An Update Application form similar to the following appears.

![null](</docs/resources/images/applications/applications-update.png>)

3. Complete the fields in the Update Application form. Required fields are denoted by an asterisk (\*).

| **Fields**                                                                                                                                             | **Description**                                                                                                                                        |
| ------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------ |
| Application Name                                                                                                                                       | Read-only field that shows the name of the application.                                                                                                |
| HTTP Method                                                                                                                                            | Select the HTTP method to be used with update operations. Choices are:                                                                                 |
| Application Specification                                                                                                                              | Select a local YAML or JSON file, enter a URL where the YAML or JSON file is located, or drag and drop the file to the location indicated in the form. |

4. Click **Submit & Deploy** to update your application automatically across ECP edge locations.<br>

    **Note:** Observe the following behaviors:

    - The application deployment process may take up to a few minutes, depending on the size of container images to be pulled, the target locations, and the number of expected instances. Once the application is deployed, **Deployed** appears as its status on the Applications page. To check the status and other details, use the applications list view and detail view. After the application is deployed, you can retrieve instances in [list view](<Retrieving Instances of an Application in List View.htm>) or [map view](<Retrieving Instances of an Application in Map View.htm>).
    - Updating an application using the method PUT replaces all existing objects, including any persistent storage volumes, of the application.
    - Scaling down or redistributing an application that uses persistent storage volumes might delete existing persistent volumes along with pod instances.