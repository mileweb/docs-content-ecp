# Updating an Application

The following procedure describes how to update applications.

1. In the left pane, click **Applications**.
2. Click the name of the application you want to update.
3. To update an application by editing the YAML file directly, click the **Edit YAML** button at the top right of the form.
4. To quickly update an application without having to touch the YAML file, click the **Update** button, select one of the following options, and refer to the appropriate section below:<ul><li> **Redistribute** allows you to add, edit, and delete distribution targets.</ul></li><ul><li>**Set container image** allows you to update your pods to a newer application version.<br></ul></li><ul><li>**Upgrade resources** allows you to upgrade the spec of your container instance to maintain performance and/or save costs.</ul></li>

![null](</docs/resources/images/applications/applications-update.png>)

## Redistributing Your Application

If you select **Redistribute** from the Quick Update drop-down list, one of two dialog boxes appears, depending on whether you elected to distribute your application per region or per PoP when you created it.

**Note:** Before proceeding, observe the following behaviors:<ul><li>The redistribution method cannot be changed using the Quick Update feature.</ul></li><ul><li>The application deployment process may take up to a few minutes, depending on the size of container images to be pulled, the target locations, and the number of expected instances. Once the application is deployed, **Deployed** appears as its status on the Applications page. To check the status and other details, use the applications list view and detail view. After the application is deployed, you can retrieve instances in [list view](</docs/portal/applications/retrieving-instances-of-an-application.md#retrieving-instances-of-an-application-in-list-view>) or [map view](</docs/portal/applications/retrieving-instances-of-an-application.md#retrieving-instances-of-an-application-in-map-view>)</ul></li><ul><li>Scaling down or redistributing an application that uses persistent storage volumes might delete existing persistent volumes along with pod instances.</li></ul></li>

### Applications Distributed per Region

If your application is distributed per region, a dialog box similar to the following appears.

![null](</docs/resources/images/applications/redistribute-your-application-distribute-per-region.png>)

1. Under **Targets**, accept or change the regions and replicas per region shown for existing targets.
2. To add targets, click the **+ Add Target** button. When a new row appears at the bottom of **Targets**, select a region and enter the number of replicas for that region.
3. To remove a target, click the trash can icon at the right side of the target.
4. When you finish, click **Redistribute**.

### Applications Distributed per PoP

If your application is distributed per PoP, a dialog box similar to the following appears.

![null](</docs/resources/images/applications/redistribute-your-application-distribute-per-pop.png>)

1. Under **Targets**, accept or change the PoPs and replicas per PoP shown for existing targets.
2. To add targets, click the **+ Add Target** button. When a new row appears at the bottom of **Targets**, select a PoP and enter the number of replicas for that PoP.
3. To remove a target, click the trash can icon at the right side of the target.
4. When you finish, click **Redistribute**.

## Setting Container Image
If you select **Set container image** from the Quick Update drop-down list, a Set Container Image dialog box similar to the following appears. 

![null](</docs/resources/images/applications/set-container-image-dialog-box.png>)

**Note:** This operation might cause your existing pods to be deleted and recreated.

1. To change the Docker image name, replace the name in the **Image** field. Typically, this name consists of docker image registry, image, and tag.
<br><ul>- If you omit the registry, the system defaults to docker hub.</ul><ul>- If you omit the tag, the system defaults to "latest".</ul><ul>- If your entry is not valid, the image pulling and application deployment fails.</ul></br>
2. To change the image pull secret, drag the <strong>Change Image Pull Secret</strong> control to the right. Then click in the field displaying the current secret and select an image pull secret.
3. To add an image pull secret, drag the <strong>Change Image Pull Secret</strong> control to the right. Click in the field displaying the current secret and select <strong>+Add Image Pull Secret</strong>. Complete the fields in the Add ImagePullSecret dialog box, and then click <strong>Submit</strong>. 
4. When you finish, click **Update**.
   
## Upgrading Resources
If you select **Upgrade resources** from the Quick Update drop-down list, an Upgrade Container Spec dialog box similar to the following appears. 

![null](</docs/resources/images/applications/upgrade-container-spec-dialog-box.png>)

**Note:** This operation might cause your existing pods to be deleted and recreated.

1. To change the number of CPU requests, enter a value in the **CPU** field. The value you enter is measured in cores. To specify millicores, add an **m** to the end of the value.
   **Note:** The CPU value should not be lower than 50 millicores, and should not cause the total amount of CPU requested by a pod to exceed 24 cores.
2. To change the number of memory requests, enter a value in the **Memory** field. The value you enter is measured in bytes. To specify a different unit of measurement, add one of the following to the end of the value: E, P, T, G, M, K, Ei, Pi, Ti, Gi, Mi, Ki.
**Note:** The memory value should not be lower than 50MB, and should not cause the total amount of memory requested by a pod to exceed 128GB.
3. When you finish, click **Upgrade**.    


    