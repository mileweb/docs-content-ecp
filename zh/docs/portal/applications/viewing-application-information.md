# Viewing Application Information and YAML Files

## Viewing Application Information

The following procedure describes how to view information about applications.

1. In the left pane, click **Applications**.
2. On the Applications page, click the name of the application whose information you want to view. A form similar to the following appears. The table below the figure describes the elements on this form.

<p align=center><img src="/docs/resources/images/applications/applications-details-basic-info-w-numbers.png" width="600"></p>

| **Fields**   | **Description**                                                                           |
| :----------: | ----------------------------------------------------------------------------------------- |
| 1            | Click this button to return to the Applications page.                                     |
| 2            | Click this button to edit the YAML file.                                                  |
| 3            | Click this button to delete the application.                                              |
| 4            | Click this button to make quick updates to the application without having to edit the corresponding YAML file. Choices are:<br><ul><li><strong>**Redistribute**</strong> = redistributes your application across ECP locations to maintain performance, save costs, or both. After an application is created, you cannot change the distribution method.<li><strong>**Set container image**</strong> = updates your pods to a newer application version. Performing this action might delete and recreate your existing pods.<li><strong>**Upgrade resources**</strong> = upgrades the spec of your container instance to maintain performance, save costs, or both. Performing this action might delete and recreate your existing pods.</br></li>        |


## Viewing YAML Files

The following procedure describes how to view YAML files from the Applications page. You can also view YAML files by clicking the **Edit YAML** button on the form used to edit application information (see the figure following step 2 above).

1. In the left pane, click **Applications**.
2. Find the application whose YAML file you want to view, then click its **Actions** menu and select **View YAML**. A Specifications dialog box similar to the following appears, where the file can be viewed in YAML or JSON format (1), copied (2), and downloaded (3). When you finish, click the **Close** (4) button.

<p align=center><img src="/docs/resources/images/applications/applications-app-spec-yaml-w-numbers.png" width="600"></p>