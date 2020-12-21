# Adding Projects

Admin portal users can use the following procedure to add projects.
**Note:** Non-admin portal users are not permitted to add projects.
1. In the left pane, click **Image Registry > Registry Projects**.
2. At the top right of the Registry Projects page, click the **\+ Add New Project** button. 
3. Complete the fields in the Add Project form. Required fields are denoted by an asterisk (\*).

![null](</docs/resources/images/registry/add-project.png>)

| **Field**              | **Description**                                 |
| -----------------------|-------------------------------------------------| 
| Project Name           | Unique name for this project. The project name can contain up to 128 characters. The name must be all lowercase alphanumeric characters, start and end with an alphanumeric character, and can contain a dash (-), underscore (_), and period (.).                    |
| Deployment Security    | Select whether to prevent images with certain vulnerability severity from being deployed. If you enable this option by dragging the slider to the right, use the drop-down list to select the level of security. Choices are:<li>negligible = ??</li><li>low = ??</li><li>medium = ??? (*default*)</li><li>high = ??</li>                                |
| Vulnerability Scan     | Select whether to scan images automatically when they are pushed to the project registry.                                   |

4. Click the **Submit** button.