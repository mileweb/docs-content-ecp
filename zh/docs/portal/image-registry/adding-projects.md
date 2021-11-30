# Adding Projects

Admin portal users can use the following procedure to add projects.

**Note:** Non-admin portal users are not permitted to add projects.

1. In the left pane, click **Image Registry > Registry Projects**.
2. At the top right of the Registry Projects page, click the **\+ Add New Project** button. 
3. Complete the fields in the Add Project form. Required fields are denoted by an asterisk (\*).

<p align=center><img src="/docs/resources/images/registry/add-project.png" width="600"></p>

| **Field**              | **Description**                                 |
| -----------------------|-------------------------------------------------| 
| Project Name           | Unique name for this project. The project name can contain up to 128 characters. The name must be all lowercase alphanumeric characters, must start and end with an alphanumeric character, and can contain dash (-), underscore (_), and period (.).                    |
| Storage Limit    | Storage quota limiting the size of all images stored under the project. The sum of storageLimits of all projects must not exceed the limit specified in your ECP serviceQuota.                                |
| Deployment Security    | Select whether to prevent images with certain vulnerability severity from being deployed. If you enable this option by dragging the slider to the right, use the drop-down list to select the level of security.                                |
| Vulnerability Scan     | Select whether to scan images automatically when they are pushed to ECP registry.                                   |

4. Click the **Submit** button.