# Adding Registry Users

Admin portal users can use the following procedure to add registry users.

**Note:** Non-admin portal users are not permitted to add registry users.

1. In the left pane, click **Image Registry > Registry Users**.
2. At the top right of the Registry Users page, click the **\+ Add New User** button. 
3. Complete the fields in the Add User form. Required fields are denoted by an asterisk (\*).

<p align=center><img src="/docs/resources/images/registry/add-user.png" width="600"></p>

| **Field**              | **Description**                                |
| -----------------------|------------------------------------------------| 
| Username           | Prefix to be used as part of the registry user's username. The username can contain up to 15 characters, and allows only lower case alphanumeric characters, ‘-’ and ‘.’. To avoid naming collisions across registry users of different customers, ECP appends a fixed-length random string to this prefix to form a complete username when it creates the new registry user.                                                            |
| Password               | Case-sensitive password for the new registry user. The password must be 8 to 20 characters long and have at least one lowercase letter, one uppercase letter, and one number.                  |
| Confirm Password       | Same case-sensitive password typed in the **Password** field.                                                      |
| Email                  | Email address for the new registry user.      |
| Description            | Optional description about the new registry user (up to 20 characters).                                                   |
| Access to Projects     | Select the projects that will be accessible to the new registry user and the new registry user's access type. Choices are:<ul><li>Allow readOnly access to all existing projects = registry user can only pull images from a project registry.</ul></li><ul><li>Allow readWrite access to all existing projects = registry user can pull images from and push images to a project registry.</ul></li><ul><li>Custom permissions = select the projects available to this registry user, and whether the registry user has readOnly or readWrite permission.</ul></li>                                    |
4. Click the **Submit** button.

**Note:** When you create an ECP registry user, a corresponding [imagePullSecret](</docs/portal/image-pull-secrets/managing-image-pull-secrets.md>) gets created automatically.