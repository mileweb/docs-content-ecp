<!--?xml version="1.0" encoding="utf-8"?-->

<link href="../Resources/TableStyles/Rows.css" rel="stylesheet" madcap:stylesheettype="table">

# Adding an ImagePullSecret

1. In the left pane, click **ImagePullSecret**.
2. At the top right of the ImagePullSecrets page, click the **\+ Add New ImagePullSecret** button. 
3. Complete the fields in the Add ImagePullSecret form. Required fields are denoted by an asterisk (\*).

<!-- -->

![null](</docs/resources/images/image-pull-secrets/Add ImagePullSecret.png>)

<span style="color: #708090; font-size: 9pt;">(click to enlarge)</span>

| **Fields**                                                                                                         | **Description**                                                                                                    |
| ------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------ |
| Name                                                                                                               | Enter a name that helps you identify this ImagePullSecret.                                                         |
| Namespace                                                                                                          | Enter the Kubernetes namespace created for your account.                                                           |
| Registry                                                                                                           | Enter the address of the registry where your container images are stored (for example, docker.io).                 |
| Username                                                                                                           | Enter the username of your registry account.                                                                       |
| Password                                                                                                           | Enter the password of your registry account. For security, each typed password character is masked with a dot (●). |
| Description                                                                                                        | Enter a description for this ImagePullSecret.                                                                      |

1. Click the **Submit** button.

<!-- -->

