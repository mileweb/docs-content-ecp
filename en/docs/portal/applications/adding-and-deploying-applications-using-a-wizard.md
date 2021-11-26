# Adding and Deploying Applications Using a Wizard

1. In the left pane of the portal, click **Applications**.
2. At the top right of the Applications page, click the **\+ Add New Application** button.

<p align=center><img src="/docs/resources/images/applications/applications.png" width="600"></p>

3. When prompted, click **Use a wizard**.
<p align=center><img src="/docs/resources/images/applications/applications-add.png" width="600"></p>

4. Complete the configure fields in the first step of the wizard.
<p align=center><img src="/docs/resources/images/applications/applications-add-wizard-configure.png" width="600"></p>

| **Fields**                                                                                                                                                                                                                              | **Description**                                                                                                                                                                                                                                                |
| -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Application Name                                                                                                                                                                                                                                               | Enter a name that helps you identify this application.                                                                                                                                                                                                         |
| Namespace                                                                                                                                                                                                                                                      | Specify a Kubernetes namespace created in the ECP clusters for your account.                                                                                                                                                                                   |
| Labels                                                                                                                                                                                                                                                         | Read-only field that shows the default label used to identify pods. The ECP uses "app" as the key and the application name you entered as the value.                                                                                                           |
| Pod Controller                                                                                                                                                                                                                                                 | Select a Kubernetes workload controller to control your pods. Choices are:<br><ul><li><strong>StatefulSet</strong> = select this option if your application requires persistent storage. </li><li><strong>Deployment</strong>.</li>                                                                                                                                                                                      |
| Image Pull Secret                                                                                                                                                                                                                                              | If your application will run private image(s), specify an ImagePullSecret that will be used to authenticate with your registry. If an ImagePullSecret is not specified or the specified ImagePullSecret is not correct, the image pulling and application deployment operations will fail. |
| Volumes                                                                                                                                                                                                                                                        | This field is available when Pod Controller is set to StatefulSet. Use this field to add one or more volumes by defining their name, storage class, and capacity.                                                                                                                                          |
| Container                                                                                                                                                                                                                                                      | Specify the container name, docker image and tag, CPU and memory resources, environment variables, and volume mounts.<br>Use Advanced Settings to define the following parameters:<br><ul><li><strong>Command</strong> = entrypoint array in JSON or YAML format. If omitted, the docker image's ENTRYPOINT is used. Variable references $(VAR_NAME) are expanded using the container's environment.</li><li><strong>Args</strong> = arguments to the entrypoint in JSON or YAML format. If omitted, the docker image's CMD is used. Variable references are expanded using the container's environment.</li><li><strong>Image Pull Policy</strong> =  control how Docker behaves when pulling images. Select from Always, Never, or IfNotPresent. Defaults to Always</li><li><strong>Liveness Probe</strong> = periodic probe of container liveliness. If the probe fails, the container will be restarted.</li><li><strong>Readiness Probe</strong> = periodic probe of container service readiness. If the probe fails, the container will be removed from service endpoints.</br></li>                                                               |

**Note:** You can add and configure multiple containers and couple them together in a pod.

5. At the top right of the wizard, click **\> Next**. 
6. Select whether to expose your application using ECP defined [layer 4 load balancer](<#exposing-via-a-load-balancer>) or the [public network interfaces of a pod](<#exposing-via-the-public-network-interfaces-of-a-pod-replica>), and then complete the remaining fields based on your selection.

<p align=center><img src="/docs/resources/images/applications/applications-add-wizard-expose.png" width="600"></p>

### Exposing via Layer 4 Load Balancer

| **Fields**                                                                                                    | **Description**                                                                                                                                            |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Name of load balancer                                                                                                                                      | Read-only field that shows the name of the load balancer. Default to same as "Application Name"                                                                                                 |
| Backend Selector                                                                                                                                           | Read-only field that selects pods to sit behind the layer 4 load balancer based on labels. The pods are what you specified in the first wizard step. |
| Listeners                                                                                                                                                  | Complete the following fields:<br><ul><li><strong>Name</strong> = enter the name of the listener. </li><li><strong>Listener Port</strong> = enter the number of the port on which the layer 4 load balancer must listen.</li> </li><li><strong>Backend Port</strong> = read-only field that shows the number of the backend pod port that receives traffic forwarded by the layer 4 load balancer. This is the same value entered for the Listener Port.</li></li><li><strong>Protocol</strong> = select either TCP or UDP.</li> </li><li><strong>Scheduler</strong> = select the load-balancing algorithm used to make load-balancing decisions. Choices are Round Robin (*default*), Least Connection and Source Hash.</li> </li><li><strong>Health Check</strong> = select whether periodic health checks should be performed on backend pods. The load balancer will remove a pod that fails the health check.</li>            |

**Note:** You can add or remove listeners by clicking the **\+ Add Listener** button or the **Remove** button.

### Exposing via the Public Network Interfaces of a Pod

| **Fields**                                               | **Description**                                                                                            |
| ---------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------- |
| Network interfaces                                                                                         | Drag the controls to the right to expose the application via a public IPv4 network, IPv6 network, or both. |

7. At the top right of the wizard, click **\> Next**. 
8. Select whether to distribute your application to ECP edge PoPs by [Region](<#distribute-per-region>) or [PoP](<#distribute-per-pop>), and then complete the remaining fields based on your selection.

<p align=center><img src="/docs/resources/images/applications/applications-add-wizard-distribute.png" width="600"></p>

### Distribute per region

| **Fields**                                                                                                                                       | **Description**                                                                                                                                                        |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Region                                                                                                                                                                 | Select an ECP Region where the application is to be distributed. The ECP will distribute your desired number of application instances across PoPs in the selected region automatically. |
| Replicas per region                                                                                                                                                    | Select the total number of application instances you want to distribute within the selected ECP Region.                                                                            |

### Distribute per PoP

| **Fields**                                               | **Description**                                                             |
| --------------------------------------------------------------------------- | --------------------------------------------------------------------------- |
| PoP                                                                         | Select one or more ECP PoPs where you want to run your application.        |
| Replicas per PoP                                                            | Select the number of application instances you want to run in each of the selected ECP PoPs. |

**Note:** You can add or remove targets by clicking the **\+ Add Target** button or the garbage can icon.

9. At the top right of the wizard, click **\> Next**. 
10. Review your inputs from the previous steps. If you need to change them, click **Previous** to return to the appropriate step, make your changes, and then click **Next** until you return to the Review step.

11. When you are satisfied with your inputs, click **Submit & Deploy**.

**Note:** The application deployment process will take a while, the length depending on the size of container images to be downloaded, the target locations, and the number of expected instances, etc. Once the application is deployed, **Deployed** appears as its status on the Applications page. To check the status and other details, use the applications list view and detail view. After the application is deployed, you can [check application instances](</docs/portal/applications/retrieving-instances-of-an-application.md>). If you encounter a problem, [try to troubleshoot](</docs/portal/applications/troubleshooting-an-application.md>).

