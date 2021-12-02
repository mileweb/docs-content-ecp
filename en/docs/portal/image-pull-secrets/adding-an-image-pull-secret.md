# Adding an ImagePullSecret

1. In the left pane, click **ImagePullSecrets**.
2. At the top right of the ImagePullSecrets page, click the **\+ Add New ImagePullSecret** button. 
3. Complete the fields in the Add ImagePullSecret form. Required fields are denoted by an asterisk (\*).

<p align=center><img src="/docs/resources/images/image-pull-secrets/image-pull-secrets-add.png" width="600"></p>

| **Fields**                                                                                                         | **Description**                                                                                                    |
| ------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------ |
| Name                                                                                                               | Enter a name that helps you identify this ImagePullSecret.                                                         |
| Registry                                                                                                           | Enter the address of the registry where your container images are stored (for example, docker.io).                 |
| Username                                                                                                           | Enter the username of your registry account.                                                                       |
| Password                                                                                                           | Enter the password of your registry account. For security, each typed password character is masked with a dot (●). |
| Description                                                                                                        | Enter a description for this ImagePullSecret.                                                                      |

4. Click the **Submit** button.

**Note:** When you [create an ECP registry user](</docs/portal/registry-users/adding-users.md>), a corresponding imagePullSecret is created automatically. Manually creating an imagePullSecret for your ECP registry user is not allowed.