# Updating an ImagePullSecret

The following procedure describes how to update an ImagePullSecret from the ImagePullSecrets page. You can also update ImagePullSecrets from the form used to [view ImagePullSecret information](</docs/portal/image-pull-secrets/viewing-image-pull-secret-information.md>).

1. In the left pane, click **ImagePullSecrets**.
2. Find the ImagePullSecret you want to update, then click its **Actions** menu and select **Update**. An Update ImagePullSecret form similar to the following appears.

<p align=center><img src="/docs/resources/images/image-pull-secrets/image-pull-secrets-update.png" width="600"></p>

3. Complete the fields in the form. Required fields are denoted by an asterisk (\*).

| **Fields**                                                                                                         | **Description**                                                                                                    |
| ------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------ |
| Name                                                                                                               | Read-only field that shows the name of this ImagePullSecret.                                                       |
| Namespace                                                                                                          | Read-only field that shows the Kubernetes namespace for your account.                                              |
| Registry                                                                                                           | Read-only field that shows the address of the registry where your container images are stored.                     |
| Username                                                                                                           | Enter the username of your registry account.                                                                       |
| Password                                                                                                           | Enter the password of your registry account. For security, each typed password character is masked with a dot (●). |
| Description                                                                                                        | Enter a description for this ImagePullSecret.                                                                      |

4. Click **Update**.

**Note:** Updating an ImagePullSecret that is being used might cause the image pull to fail temporarily.