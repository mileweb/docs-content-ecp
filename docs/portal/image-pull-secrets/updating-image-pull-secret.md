<!--?xml version="1.0" encoding="utf-8"?-->

<link href="../Resources/TableStyles/Rows.css" rel="stylesheet" madcap:stylesheettype="table">

# Updating an ImagePullSecret

The following procedure describes how to update an ImagePullSecret from the ImagePullSecrets page. You can also update ImagePullSecrets from the form used to [view ImagePullSecret information](<Viewing ImagePullSecret Information.htm>).

1. In the left pane, click **ImagePullSecrets**.
2. Find the ImagePullSecret you want to update, then click its **Actions** menu and select **Update**. An Update ImagePullSecret form similar to the following appears.

<!-- -->

![null](</docs/resources/images/image-pull-secrets/Update ImagePullSecret.png>)

<span style="color: #708090; font-size: 9pt;">(click to enlarge)</span>

1. Complete the fields in the form. Required fields are denoted by an asterisk (\*).

<!-- -->

| **Fields**                                                                                                         | **Description**                                                                                                    |
| ------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------ |
| Name                                                                                                               | Read-only field that shows the name of this ImagePullSecret.                                                       |
| Namespace                                                                                                          | Read-only field that shows the Kubernetes namespace for your account.                                              |
| Registry                                                                                                           | Read-only field that shows the address of the registry where your container images are stored.                     |
| Username                                                                                                           | Enter the username of your registry account.                                                                       |
| Password                                                                                                           | Enter the password of your registry account. For security, each typed password character is masked with a dot (●). |
| Description                                                                                                        | Enter a description for this ImagePullSecret.                                                                      |

1. Click **Update**.

<!-- -->

**Note:** Updating an ImagePullSecret that is being used might cause the image pull to fail temporarily.







