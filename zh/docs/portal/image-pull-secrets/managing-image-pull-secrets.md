# Managing ImagePullSecrets

The concept of an ImagePullSecret is similar to the one native to [Kubernetes](<https://kubernetes.io/docs/tasks/configure-pod-container/pull-image-private-registry/>). An ImagePullSecret is an authorization token (or "secret") that stores Docker credentials that are used to access a registry. If your application uses private image(s), ECP clusters will require such an ImagePullSecret so as to authenticate with your container registry when pulling your private image(s) from there. You do not need to create the ImagePullSecret in ECP clusters. All you need to do is to pass the registry address and your registry account to the ECP. The ECP API server, in turn, creates a corresponding ImagePullSecret in the ECP clusters where your application will be deployed.

Observe the following guidelines:

- An `ImagePullSecret` is required only if your containerized application uses image(s) stored in a private repository. Pulling an image from a public repository does not require registry authentication, so no `ImagePullSecret` is needed.
- If your containerized application will use a private image, create an `ImagePullSecret` before configuring and deploying the application. Otherwise, the subsequent image pull will fail. 
- After you pass your registry address and account, the ECP API server creates and maintains in ECP clusters an `ImagePullSecret` representing the info passed. The ECP API server does not validate the registry address and account. You are responsible for the accuracy and validity of this information. An `ImagePullSecret` with invalid registry information causes image pulls to fail.
- The ECP platform does not impose restrictions on what image registries can be used. You can use either public registries like docker hub or your own registries. Alternately, you can use our ECP registry, which is shipped with other ECP key features.

### ImagePullSecrets Page 

ImagePullSecrets are managed from the ImagePullSecrets page. To display this page, click **ImagePullSecrets** in the left pane.

The following figure shows the key elements on the page, and the table following the figure describes them.

<p align=center><img src="/docs/resources/images/image-pull-secrets/image-pull-secrets-w-numbers.png" width="700"></p>

| **Fields**   | **Description**                                                                                           |
| :----------: | --------------------------------------------------------------------------------------------------------- |
| 1            | To filter ImagePullSecrets, type characters in this field and then press the Enter key. All ImagePullSecrets that do not contain the typed characters are hidden. Filtering is not case-sensitive. To remove the filter, click the **Reset** button.                                 |
| 2            | Each ImagePullSecret appears on its own row. Clicking an ImagePullSecret allows you to view more information about the ImagePullSecret.                                                                                                           |
| 3            | The Actions drop-down list on each row has options to [update](</docs/portal/image-pull-secrets/updating-image-pull-secret.md>) or [delete](</docs/portal/image-pull-secrets/deleting-an-image-pull-secret.md>) an ImagePullSecret.                                                  |
| 4            | The **+ Add New ImagePullSecret** button allows you to [add](</docs/portal/image-pull-secrets/adding-an-image-pull-secret.md>) ImagePullSecrets.                                                                                                          |

**Note:** ImagePullSecrets automatically created for your ECP register users (if any) are also shown on the list. Such ImagePullSecrets are managed by the ECP and cannot be updated or deleted.