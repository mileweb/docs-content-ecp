# Adding and Deploying Applications Using a Wizard

1. In the left pane of the portal, click **Applications**.
2. At the top right of the Applications page, click the **\+ Add New Application** button.

![null](</docs/resources/images/applications/applications.png>)

3. When prompted, click **Use a wizard**.

![null](</docs/resources/images/applications/applications-add.png>)

4. Complete the configure fields in the first page of the wizard.

![null](</docs/resources/images/applications/applications-add-wizard-configure.png>)

| **Wizard Fields: Configure Page**                                                                                                                                                                                                                              | **Description**                                                                                                                                                                                                                                                |
| -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Application Name                                                                                                                                                                                                                                               | Enter a name that helps you identify this application.                                                                                                                                                                                                         |
| Namespace                                                                                                                                                                                                                                                      | Specify a Kubernetes namespace created in the ECP clusters for your account.                                                                                                                                                                                   |
| Labels                                                                                                                                                                                                                                                         | Read-only field that shows the default label used to identify pods. The ECP uses "app" as the key and the application name you entered as the value.                                                                                                           |
| Pod Controller                                                                                                                                                                                                                                                 | Select a Kubernetes workload controller to control your pods. Choices are:<br><ul><li><strong>StatefulSet</strong> = select this option if your application requires persistent storage. </li><li><strong>Deployment</strong>.</li>                                                                                                                                                                                      |
| Image Pull Secret                                                                                                                                                                                                                                              | If your application will run private image(s), specify an ImagePullSecret that will be used to authenticate with your registry. If the specified ImagePullSecret is not correct or missing, the image pulling and application deployment operations will fail. |
| Volumes                                                                                                                                                                                                                                                        | If Pod Controller is set to StatefulSet, add one or more volumes by defining their name, storage class, and capacity.                                                                                                                                          |
| Container                                                                                                                                                                                                                                                      | Specify the container name, docker image and tag, CPU and memory resources, environment variables, and volume mounts for the first container (Container0).<br>Use Advanced Settings to define the following parameters:<br><ul><li><strong>Command</strong> = entrypoint array in JSON or YAML format. If omitted, the docker image's ENTRYPOINT is used. Variable references $(VAR_NAME) are expanded using the container's environment.</li><li><strong>Args</strong> = arguments to the entrypoint in JSON or YAML format. If omitted, the docker image's CMD is used. Variable references are expanded using the container's environment.</li><li><strong>Image Pull Policy</strong> =  select from Always, Never, or IfNotPresent. If latest tag is specified, this setting defaults to Always; otherwise, it defaults to IfNotPresent</li><li><strong>Liveness Probe</strong> = periodic probe of container liveliness. If the probe fails, the container will be restarted.</li><li><strong>Readiness Probe</strong> = periodic probe of container service readiness. If the probe fails, the container will be removed from service endpoints.</br></li>                                                               |

**Note:** You can add containers, environment variables, and volume mounts by clicking their **\+ Add** links in the **Container** section.

5. At the top right of the wizard, click **\> Next**. 
6. Select whether to expose your application using a [Layer 4 load balancer](<#exposing-via-a-load-balancer>) or the [public network interfaces of a pod replica](<#exposing-via-the-public-network>), and then complete the remaining fields based on your selection.

![null](</docs/resources/images/applications/applications-add-wizard-expose.png>)

### Exposing via a Load Balancer

| **Fields for Exposing Application via a Load Balancer**                                                                                                    | **Description**                                                                                                                                            |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Name of load balancer                                                                                                                                      | Read-only field that shows the name of the load balancer.                                                                                                  |
| Backend Selector                                                                                                                                           | Read-only field that shows the pods located behind the layer 4 load balancer based on labels. These are the pods you specified in the first wizard screen. |
| Listeners                                                                                                                                                  | Complete the following fields:<br><ul><li><strong>Name</strong> = enter the name of the listener. </li><li><strong>Listener Port</strong> = enter the number of the port on which the layer 4 load balancer must listen.</li> </li><li><strong>Backend Port</strong> = read-only field that shows the number of the backend pod port that receives traffic forwarded by the layer 4 load balancer. This is the same value entered for the Listener Port.</li></li><li><strong>Protocol</strong> = select either TCP or UDP.</li> </li><li><strong>Scheduler</strong> = select the load-balancing algorithm used to make load-balancing decisions. Choices are Round Robin (*default*) or Least Connection.</li> </li><li><strong>Health Check</strong> = select whether periodic health checks should be performed on backend pods. The load balancer will remove a pod that fails the health check.</li>            |

**Note:** You can add or remove listeners by clicking the **\+ Add Listener** link or the **Remove** button.

### Exposing via the Public Network Interfaces of a Pod Replica

| Fields for **Exposing Application via the Public Network**                                                 | **Description**                                                                                            |
| ---------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------- |
| Network interfaces                                                                                         | Drag the controls to the right to expose the application via a public IPv4 network, IPv6 network, or both. |

7. At the top right of the wizard, click **\> Next**. 
8. Select whether to distribute your application to ECP edge PoPs by [region](<#distribute-per-region>) or [PoP](<#distribute-per-pop>), and then complete the remaining fields based on your selection.

![null](</docs/resources/images/applications/applications-add-wizard-distribute.png>)

### Distribute per region

| **Distribute per Region Fields**                                                                                                                                       | **Description**                                                                                                                                                        |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Region                                                                                                                                                                 | Select an ECP region where the application is to be distributed. The ECP scheduler will distribute your pod replicas across PoPs in the selected region automatically. |
| Replicas per region                                                                                                                                                    | Select the total number of pod replicas you want to distribute within the selected ECP region.                                                                            |

### Distribute per PoP

| **Distribute per PoP Fields**                                               | **Description**                                                             |
| --------------------------------------------------------------------------- | --------------------------------------------------------------------------- |
| PoP                                                                         | Select one or more ECP PoPs where you want to run your pod replicas.        |
| Replicas per PoP                                                            | Select the number of pod replicas you want to run in the selected ECP PoPs. |

**Note:** You can add or remove targets by clicking the **\+ Add Target** link or the garbage can icon.

9. At the top right of the wizard, click **\> Next**. 
10. Review your selections from the previous steps. If you need to change them, click **Previous** to return to the appropriate step, make your changes, and then click **Next** until you return to the Review step.

11. When you are satisfied with your selections, click **Submit & Deploy**.

**Note:** The application deployment process may take a few minutes, depending on the size of container images to be pulled, the target locations, and the number of expected instances. Once the application is deployed, **Deployed** appears as its status on the Applications page. To check the status and other details, use the applications list view and detail view. After the application is deployed, you can retrieve instances in [list view](</docs/portal/applications/retrieving-instances-of-an-application.md#retrieving-instances-of-an-application-in-list-view>) or [map view](</docs/portal/applications/retrieving-instances-of-an-application.md#retrieving-instances-of-an-application-in-map-view>). If you encounter a problem, [troubleshoot the application](</docs/portal/applications/troubleshooting-an-application.md>).

