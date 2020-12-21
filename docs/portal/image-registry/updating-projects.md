# Updating Projects

Updating a project allows admin portal users to change its deployment security and vulnerability scan settings. The following procedure describes how to update projects. To make sure the appropriate project is updated, the project can be viewed before it is updated.
**Note:** Non-admin portal users are not permitted to upgrade projects.
1. In the left pane, click **Image Registry > Registry Projects**.
2. Perform one of the following tasks:<ul><li>To update a project from the Registry Projects page, click its **Actions** button and select **Update**. </ul></li> <ul><li>To view information about a project before updating it, click its name to display the Edit page. To update the project, click the **Update** button at the top right.</ul></li>
      ![null](</docs/resources/images/registry/update-project.png>)
3. Change the settings as necessary.
   
| **Field**              | **Description**                                                                                 |
| -----------------------|-------------------------------------------------------------------------------------------------| 
| Project Name           | Read-only field that shows the unique name of this project.                                    |
| Deployment Security    | Select whether to prevent images with certain vulnerability severity from being deployed. If you enable this option by dragging the slider to the right, use the drop-down list to select the level of security. Choices are:<li>negligible = ??</li><li>low = ??</li><li>medium = ??? (*default*)</li><li>high = ??       |
| Vulnerability Scan     | Select whether to scan images automatically when they are pushed to the project registry.       |
4. Click **Submit**.