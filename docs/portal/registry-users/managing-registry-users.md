# Managing Registry Users

A registry user is an entity that is created and given certain permissions to access and manage repositories and tags in the registry. Usually, a registry user uses the docker CLI client to access an image registry.

## Registry Users Page
Registry users are managed from the Registry Users page. To display this page, click **Image Registry > Registry Users** in the left pane.

The following figure shows the key elements on the page, and the table following the figure describes them.

<p align=center><img src="/docs/resources/images/registry/registry-users-page.png" width="700">


| **Element Number**       | **Description**                               |
| -------------------------|-----------------------------------------------| 
1                                                                                                       | To filter registry users, type characters in this field and then press the Enter key. All registry users that do not contain the typed characters are hidden. Filtering is not case-sensitive. To remove the filter, click the **Reset** button.                                             |
| 2                        | Each registry user appears on its own row. Clicking a registry user allows you to view basic information about the registry user and the projects associated with the user.             |
| 3                        | The **Actions** drop-down list on each row has options to [update the registry user](</docs/portal/registry-users/updating-users.md>), [change the registry user's password](</docs/portal/registry-users/changing-passwords.md>), and [delete the registry user](</docs/portal/registry-users/deleting-users.md>).                                                                          |
| 4                        | The **+ Add New User** button allows you to [add registry users](</docs/portal/registry-users/adding-users.md>).          |