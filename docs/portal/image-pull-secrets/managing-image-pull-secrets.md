<!--?xml version="1.0" encoding="utf-8"?-->

<link href="../Resources/TableStyles/Rows.css" rel="stylesheet" madcap:stylesheettype="table">

<title>Certificates Overview</title>

# Managing ImagePullSecrets

The concept of an ImagePullSecret is similar to the one that is native to [Kubernetes](<https://kubernetes.io/docs/tasks/configure-pod-container/pull-image-private-registry/>). An ImagePullSecret is an authorization token (or "secret") that stores Docker credentials that are used to access a registry. ECP clusters use a secret of type “docker-registry” to authenticate with your container registry and pull a private image for your application. You do not have to create the ImagePullSecret in ECP clusters. All you need to do is pass the registry address and your registry account to the ECP. The ECP API server, in turn, creates a corresponding ImagePullSecret in the ECP clusters where your application will be deployed.

Observe the following guidelines:

- An <span style="font-family: 'Courier New';">ImagePullSecret</span>

 is required only if your containerized application will use a private image. Pulling a public image does not require registry authentication, so no <span style="font-family: 'Courier New';">ImagePullSecret</span>

 is needed.
- If your containerized application will use a private image, create an <span style="font-family: 'Courier New';">ImagePullSecret</span>

 before configuring and deploying the application. Otherwise, the subsequent image pull will fail.
- When you pass your registry address and account, the ECP API server creates and maintains the <span style="font-family: 'Courier New';">ImagePullSecret</span>

 in ECP clusters. The ECP API server does not validate the registry address and account. You are responsible for the accuracy and validity of this information. An <span style="font-family: 'Courier New';">ImagePullSecret</span>

 with invalid registry information causes image pulls to fail.
- The ECP platform does not impose restrictions on what image registries can be used. You can use public registries like docker hub or your own registries. Alternatively, you can use our ECP registry, which comes with ECP key features. For more information, contact CDNetworks.

<!-- -->



### ImagePullSecrets Page 

ImagePullSecrets are managed from the ImagePullSecrets page. To display this page, click **ImagePullSecrets** in the left pane.

The following figure shows the key elements on the page, and the table following the figure describes them.

![null](</docs/resources/images/image-pull-secrets/Managing ImagePullSecrets.png>)

<span style="color: #708090; font-size: 9pt;">(click to enlarge)</span>

|  |
|  |
|  |
|  |
|  |
|  |

