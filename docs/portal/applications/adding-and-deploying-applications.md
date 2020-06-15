<!--?xml version="1.0" encoding="utf-8"?-->

<link href="../Resources/TableStyles/Rows.css" rel="stylesheet" madcap:stylesheettype="table">

# Adding and Deploying Applications Using a Wizard

1. In the left pane of the Portal, click **Applications**.
2. At the top right of the Applications page, click the **\+ Add New Application** button.

<!-- -->

![null](</docs/resources/images/applications/Add Application.png>)

<span style="color: #708090; font-size: 9pt;">(click to enlarge)</span>

3. When prompted, click **Use a wizard**.

<!-- -->

![null](</docs/resources/images/applications/Add New Application.png>)

4. Complete the configure fields in the first page of the wizard.

<!-- -->

![null](</docs/resources/images/applications/Add New Application - Wizard 1.png>)

<span style="color: #708090; font-size: 9pt;">(click to enlarge)</span>

| **Wizard Fields: Configure Page**                                                                                                                                                                                                                              | **Description**                                                                                                                                                                                                                                                |
| -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Application Name                                                                                                                                                                                                                                               | Enter a name that helps you identify this application.                                                                                                                                                                                                         |
| Namespace                                                                                                                                                                                                                                                      | Specify a Kubernetes namespace created in the ECP clusters for your account.                                                                                                                                                                                   |
| Labels                                                                                                                                                                                                                                                         | Read-only field that shows the default label used to identify pods. The ECP uses "app" as the key and the application name you entered as the value.                                                                                                           |
| Pod Controller                                                                                                                                                                                                                                                 | Select a Kubernetes workload controller to control your pods. Choices are:                                                                                                                                                                                     |
|                                                                                                                                                                                                                                                                |                                                                                                                                                                                                                                                                |
| Image Pull Secret                                                                                                                                                                                                                                              | If your application will run private image(s), specify an ImagePullSecret that will be used to authenticate with your registry. If the specified ImagePullSecret is not correct or missing, the image pulling and application deployment operations will fail. |
| Restart Policy                                                                                                                                                                                                                                                 | Select the Restart policy for all containers within a pod. Choices are:                                                                                                                                                                                        |
|                                                                                                                                                                                                                                                                |                                                                                                                                                                                                                                                                |
| Volumes                                                                                                                                                                                                                                                        | If Pod Controller is set to StatefulSet, add one or more volumes by defining their name, storage class, and capacity.                                                                                                                                          |
| Container                                                                                                                                                                                                                                                      | Specify the container name, docker image and tag, CPU and memory resources, environment variables, and volume mounts for the first container (**Container0**). Use Advanced Settings to define:                                                                |
|                                                                                                                                                                                                                                                                |                                                                                                                                                                                                                                                                |



**Note:** You can add containers, environment variables, and volume mounts by clicking their **\+ Add** links in the **Container** section.

1. At the top right of the wizard, click **\> Next**. 
2. Select whether to expose your application using a [Layer 4 load balancer](<#Exposedlayer4>) or the[ public network](<#PublicNetwork>), and then complete the remaining fields based on your selection.

<!-- -->

![null](</docs/resources/images/applications/Add New Application - Wizard 2.png>)

<span style="color: #708090; font-size: 9pt;">(click to enlarge)</span>

| **Fields for Exposing Application via a Load Balancer**                                                                                                    | **Description**                                                                                                                                            |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Name of load balancer                                                                                                                                      | Read-only field that shows the name of the load balancer.                                                                                                  |
| Backend Selector                                                                                                                                           | Read-only field that shows the pods located behind the layer 4 load balancer based on labels. These are the pods you specified in the first wizard screen. |
| Listeners                                                                                                                                                  | Complete the following fields:                                                                                                                             |
|                                                                                                                                                            |                                                                                                                                                            |

**Note:** You can add or remove listeners by clicking the **\+ Add Listener** link or the **Remove** button.

| Fields for **Exposing Application via the Public Network**                                                 | **Description**                                                                                            |
| ---------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------- |
| Network interfaces                                                                                         | Drag the controls to the right to expose the application via a public IPv4 network, IPv6 network, or both. |

1. At the top right of the wizard, click **\> Next**. 
2. Select whether to distribute your application to ECP edge PoPs by [region](<#DistributebyRegion>) or [PoP](<#DistributebyPoPFields>), and then complete the remaining fields based on your selection.

<!-- -->

![null](</docs/resources/images/applications/Add New Application - Wizard 3.png>)

<span style="color: #708090; font-size: 9pt;">(click to enlarge)</span>

| **Distribute per Region Fields**                                                                                                                                       | **Description**                                                                                                                                                        |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Region                                                                                                                                                                 | Select an ECP region where the application is to be distributed. The ECP scheduler will distribute your pod replicas across PoPs in the selected region automatically. |
| Replicas per region                                                                                                                                                    | Select the total number of pod replicas you want distribute within the selected ECP region.                                                                            |



| **Distribute per PoP Fields**                                               | **Description**                                                             |
| --------------------------------------------------------------------------- | --------------------------------------------------------------------------- |
| PoP                                                                         | Select one or more ECP PoPs where you want to run your pod replicas.        |
| Replicas per PoP                                                            | Select the number of pod replicas you want to run in the selected ECP PoPs. |

**Note:** You can add or remove targets by clicking the **\+ Add Target** link or the garbage can icon.

1. At the top right of the wizard, click **\> Next**. 
2. Review your selections from the previous steps. If you need to change them, click **Previous** to return to the appropriate step, make your changes, and then click **Next** until you return to the Review step.

<!-- -->

1. When you are satisfied with your selections, click **Submit & Deploy**.

<!-- -->

**Note:** The application deployment process may take up to a few minutes, depending on the size of container images to be pulled, the target locations, and the number of expected instances. Once the application is deployed, **Deployed** appears as its status on the Applications page. To check the status and other details, use the applications list view and detail view. After the application is deployed, you can retrieve instances in [list view](<Retrieving Instances of an Application in List View.htm>) or [map view](<Retrieving Instances of an Application in Map View.htm>). If you encounter a problem, [troubleshoot the application](<Troubleshooting an Application.htm>).


<!--?xml version="1.0" encoding="utf-8"?-->

# Configuring Applications

The first step in deploying your application to ECP clusters is to use the ECP-defined “Application” object. An ECP “Application” typically consists of a target, a Kubernetes workload controller, and a Layer 4 load balancer.

## Target

The target specifies where you want to run your application and the number of instances expected. Two target options are supported. The first option allows you to pick ECP locations that best fit your requirements by using the type <span style="font-family: 'Courier New';">Location</span>

. Alternatively, if you want to distribute your application within a region and want the ECP to pick locations automatically for you, use the type <span style="font-family: 'Courier New';">RegionPreference</span>

.

The following examples show how to configure different types of targets.

### Target of type “Location”

```yaml
apiVersion: v1
kind: Location # use ECP defined Location object to specify target locations and desired number of instances
metadata:
  namespace: demo # the kubernetes namespace created for your account
spec:
  locations:
  - name: mia # use ECP PoP code to specify an ECP location
    replicas: 1 # specify the count of instances to be deployed to an ECP location
  - name: icn
    replicas: 2
```

### Target of type “RegionPreference”

```yaml
apiVersion: v1
kind: RegionPreference # use ECP defined RegionPreference object to specify target regions and desired number of instances
metadata:
  namespace: demo # the kubernetes namespace created for your account
spec:
  regions:
  - name: NA-WEST # use ECP region code to specify an ECP region
    replicas: 8 # specify number of instances to be distributed across locations in an ECP region
  - name: APAC
    replicas: 5
```

## Kubernetes Workload Controller

The Kubernetes workload controller controls the state of an application instance. It includes specifications for the container image, compute/storage resources request, container startup commands and args, etc. The workload controller is configured the same as the [native Kubernetes Controller](<https://kubernetes.io/docs/concepts/workloads/controllers/replicaset/>).

## Layer 4 Load Balancer

To expose your application, we recommend you use a Layer 4 load balancer as a frontend for your pods, unless there are special requirements to expose the pods directly. Unlike native Kubernetes, which defines a Service object for service discovery and load balancing of an application, the ECP offers a self-defined <span style="font-family: 'Courier New';">LoadBalancer4</span>

 object to help you expose your application and load balance traffic. For more information, click [here](<file:///G:/Manuals/CD Networks/Job 2 - Edge Computing Product (ECP) Project/CDNECP OnlineHelp/Content/Applications/Using Advanced ECP Features in Your Applications.htm#Using>).

## Sample Demo Configuration

The following example shows a demo configuration of an ECP application. In this example, the application will be deployed to two ECP locations, with some instances using the <span style="font-family: 'Courier New';">Location</span>

 object. This example uses a <span style="font-family: 'Courier New';">StatefulSet</span>

 controller to declare that a container running NGINX web server will be spun up, with some compute/storage resources provisioned. It also exposes the NGINX containers and defines traffic-forwarding rules using the <span style="font-family: 'Courier New';">LoadBalancer4</span>

 object.

```yaml
apiVersion: v1
kind: Location # specify target locations and desired number of instances
metadata:
  namespace: demo # the kubernetes namespace created for your account
spec:
  locations:
  - name: mia # use ECP PoP code to specify an ECP location
    replicas: 1 # instances to be deployed to an ECP location
  - name: icn
    replicas: 2
---
apiVersion: apps/v1
kind: StatefulSet # specify a kubernetes workload controller. Can be StatefulSet or Deployment. Please use StatefulSet if persistent storage is required.
metadata:
  namespace: demo # the kubernetes namespace created for your account
spec:
  selector:
    matchLabels:
      app: demoapp
  template:
    metadata:
      labels:
        app: demoapp
    spec:
      imagePullSecrets: # required only if a private image is to be pulled
      - name: myregistrykey # create this before referencing to it here, if a private image is to be pulled
      containers:
      - image: nginx # url to an image, e.g. hub.docker.com/project1/demo:latest. Default registry is dockerhub.
        name: demoapp
        resources:
          limits:
            cpu: "200m"
            memory: 256Mi
          requests:
            cpu: "200m"
            memory: 256Mi
        volumeMounts: # mount a persistent volume to a container. Optional.
        - mountPath: /tmp
          name: data
  volumeClaimTemplates: # request for a persistent volume if persistent storage is required. Optional.
  - metadata:
      annotations:
        volume.beta.kubernetes.io/storage-class: local-ssd # ECP defined storage-class. "local-ssd" means local SSD storage.
      name: data
    spec:
      accessModes:
      - ReadWriteOnce
      resources:
        requests:
          storage: 1G
---
apiVersion: v1
kind: LoadBalancer4 # ECP defined layer 4 load balancer. Use this to expose your app.
metadata: 
  namespace: demo # the kubernetes namespace created for your account
spec: 
  listeners: # specify traffic forward rules
  - backendPort: 80 # port of backend pod replicas that receive forwarded traffic
    backendSelector: # select pod replicas that sit behind this layer 4 load balancer
      app: demoapp
    healthCheck: false 
    listenerPort: 80 # port that this layer 4 load balancer listens on
    name: listener-80
    protocol: tcp
    scheduler: lc

```



Observe the following guidelines:

- The ECP accepts application configurations in JSON or YAML format. Like Kubernetes, YAML is the preferred format.
- Wrap the elements of an ECP application into a single JSON or YAML file before submitting to the ECP. PATCHing an existing application allows partial configuration updates for a specific element of the application.
- An “application name” parameter is required when an application configuration is to be deployed. The value of this parameter is used to fill the <span style="font-family: 'Courier New';">metadata.name</span>

 fields of the target, workload controller, and <span style="font-family: 'Courier New';">LoadBalancer4</span>

 objects. If you specify these <span style="font-family: 'Courier New';">metadata.name</span>

” fields in the application configuration, make sure the values are consistent with the “application name” parameter.
- The target type must be either <span style="font-family: 'Courier New';">Location</span>

 or <span style="font-family: 'Courier New';">RegionPreference</span>

. Mixed usage of the two types is not allowed. Because some ECP locations / regions might not be enabled for you, contact CDNetworks' sales engineers if you want to enable certain locations or regions, or if you have trouble deploying your application to ECP locations/regions.
- Not all Kubernetes workload Controllers are supported. CDNetworks recommends you use a [StatefulSet](<https://kubernetes.io/docs/concepts/workloads/controllers/statefulset/>) Controller to run applications that require persistent storage. Otherwise, use a [ReplicaSet](<https://kubernetes.io/docs/concepts/workloads/controllers/replicaset/>) Controller.
- When configuring a workload Controller, leave the <span style="font-family: 'Courier New';">spec.replicas</span>

 field empty because the equivalent is configured in the target object.
- If you need persistent volumes for your application, you can use two storage classes: <span style="font-family: 'Courier New';">local-ssd</span>

 and <span style="font-family: 'Courier New';">persist-ssd</span>

. For more information, see [Using Storage Resources](<Using Advanced ECP Features in Your Applications.htm#UsingStorageResources>).
- Running containers in privileged mode is not allowed.

<!-- -->



<!--?xml version="1.0" encoding="utf-8"?-->

# Uploading a YAML/JSON File



1. [Configure an application](<Configuring applications.htm>) outside of the Portal.
2. In the left pane of the Portal, click **Applications**.
3. At the top right of the Applications page, click the **\+ Add New Application** button. 

<!-- -->



![null](</docs/resources/images/applications/Add Application.png>)

<span style="color: #708090; font-size: 9pt;">(click to enlarge)</span>

4. When prompted, click **Use your YAML/JSON**.

<!-- -->

![null](</docs/resources/images/applications/Add New Application.png>)

1. In the **Application Name** field, enter a name that helps you identify this application.
2. In the **Application Specification** field, upload the local YAML or JSON file, enter a URL that points to the file, or drag and drop the file into the designated location on the form.

3. Click **Submit & Deploy**.<br>

<br>

**Note:** The application deployment process may take up to a few minutes, depending on the size of container images to be pulled, the target locations, and the number of expected instances. Once the application is deployed, **Deployed** appears as its status on the Applications page. To check the status and other details, use the applications list view and detail view. After the application is deployed, you can retrieve instances in [list view](<Retrieving Instances of an Application in List View.htm>) or [map view](<Retrieving Instances of an Application in Map View.htm>). If you encounter a problem, [troubleshoot the application](<Troubleshooting an Application.htm>).

<!-- -->

![null](</docs/resources/images/applications/Add New Application - Upload File.png>)

<span style="color: #708090; font-size: 9pt;">(click to enlarge)</span>


<!--?xml version="1.0" encoding="utf-8"?-->

# Using Advanced ECP Features

## Request Public IP Address for a Pod

When a pod gets created with the native Kubernetes, the pod is assigned a private IP address that is accessible only from within the Kubernetes cluster. CDNetworks’ ECP extensions to Kubernetes allow you to request a public IP address for a pod and support IPv4 and IPv6 protocols.

### Request Public IPv4 Address

To obtain a public IPv4 address for your pod, add an annotation to the pod spec, as marked in blue in the following YAML file example.

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: myapp
  namespace: demo
spec:
  selector:
    matchLabels:
      app: myapp
  template:
    metadata:
      labels:
        app: myapp
      annotations:
        quantil.com/enableExternalIP: "true" # add this annotation to request a public IPv4 address for a pod
    spec:
      containers:
      - image: nginx
        name: myapp
        resources:
          limits:
            cpu: "200m"
            memory: 256Mi
          requests:
            cpu: "200m"
            memory: 256Mi
```

### Request Public IPv6 Address

To obtain a public IPv6 address for your pod, add an annotation to the pod spec, as marked in blue in the following YAML file example.

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: myapp
  namespace: demo
spec:
  selector:
    matchLabels:
      app: myapp
  template:
    metadata:
      labels:
        app: myapp
      annotations:
        quantil.com/enableIpv6ExternalIP: "true" # add this annotation to request a public IPv6 address for a pod
    spec:
      containers:
      - image: nginx
        name: myapp
        resources:
          limits:
            cpu: "200m"
            memory: 256Mi
          requests:
            cpu: "200m"
            memory: 256Mi
```



## Using Layer 4 Load Balancing

To expose your application, a Layer 4 load balancer is recommended for use as a frontend for your pods, unless there are special requirements to expose the pods directly. Refer to the following example.

```yaml
apiVersion: v1
kind: LoadBalancer4 # ECP defined layer 4 load balancer.
metadata:
  name: demo-lb4 
  namespace: demo # the kubernetes namespace created for your account
spec: 
  listeners:
  - backendPort: 80 # port of backend pods to receive forwarded traffic
    backendSelector: # select backend pods based on pod labels
      app: demoapp
    healthCheck: false # turn on/off health check. Set to false by default.
    listenerPort: 80 # port exposed by the layer 4 load balancer. Must be the same as “backendPort”.
    name: listener-80
    protocol: tcp # can be “tcp” or “udp”
    scheduler: lc # scheduling policy. Can be “lc”, or “rr”. Set to “lc” by default
```

### Load Balancer Health Checks

You can configure TCP, UDP, and HTTP health checks for your Layer 4 load balancer.


**TCP Health Check**

```yaml
apiVersion: v1
kind: LoadBalancer4
metadata:
  name: demo-lb4 
  namespace: demo
spec: 
  listeners:
  - backendPort: 80
    backendSelector:
      app: demoapp
    healthCheck: true
    healthCheckType: tcp # can be “tcp” or “http”. “tcp” by default.
    healthCheckConnectPort: 80 # same as backendPort by default
    healthCheckTimeout: 10 # 10 by default. Scope: 1-50 in seconds
    unhealthyThreshold: 3 # 3 by default. Must be a positive integer
    healthCheckInterval: 1 # 1 by default. Scope: 1-5  in seconds
    listenerPort: 80
    name: listener-80
    protocol: tcp
    scheduler: lc
```


**UDP Health Check**

```yaml
apiVersion: v1
kind: LoadBalancer4
metadata:
  name: demo-lb4 
  namespace: demo
spec: 
  listeners:
  - backendPort: 80
    backendSelector:
      app: demoapp
    healthCheck: true
    healthCheckType: udp  # “tcp” by default, please set it to “udp”.
    healthCheckConnectPort: 80 # same as backendPort by default
    healthCheckTimeout: 10 # 10 by default. Scope: 1-50 in seconds
    unhealthyThreshold: 3 # 3 by default. Must be a positive integer
    healthCheckInterval: 1 # 1 by default. Scope: 1-5  in seconds
    listenerPort: 80
    name: listener-80
    protocol: udp # “healthCheckType” must be “udp” if the “protocol” here is “udp”
    scheduler: lc
```


**HTTP Health Check**

```yaml
apiVersion: v1
kind: LoadBalancer4
metadata:
  name: demo-lb4 
  namespace: demo
spec: 
  listeners:
  - backendPort: 80
    backendSelector:
      app: demoapp
    healthCheck: true
    healthCheckType: http # “tcp” by default. Please set it to “http”.
    healthCheckDomain: "foo.bar.com"
    healthCheckURI: "/index.html"
    healthCheckConnectPort: 80 # same as backendPort by default
    healthCheckTimeout: 10 # 10 by default. Scope: 1-50 in seconds
    unhealthyThreshold: 3 # 3 by default. Must be a positive integer
    healthCheckInterval: 1 # 1 by default. Scope: 1-5  in seconds
    listenerPort: 80
    name: listener-80
    protocol: tcp
    scheduler: lc
```



## Using Storage Resources

The ECP platform defines two storage classes for different use cases of persistent storage:

- `local-ssd`

- `persist-ssd`


<!-- -->

<span style="font-family: 'Courier New';">local-ssd</span>

 is for local SSD storage. Data persists through container restarts and in-node recreations, but is lost when the pod is rescheduled to other nodes.

<span style="font-family: 'Courier New';">persist-ssd</span>

 is for persistent SSD block storage. <span style="font-family: 'Courier New';">persist-ssd</span>

 is similar to Amazon Web Services EBS. Data persists through container restarts and recreations, even when the pod is rescheduled to other nodes.

Observe the following guidelines:

- If persistent volumes are required, use <span style="font-family: 'Courier New';">StatefulSet <span style="font-family: Arial;">Controller</span></span>

 for your application.
- The requested capacity of a single <span style="font-family: 'Courier New';">persistentVolumeClaim</span>

 (PVC) must be between 500MB and 100GB.
- You cannot use <span style="font-family: 'Courier New';">local-ssd</span>

 and <span style="font-family: 'Courier New';">persist-ssd</span>

 volumes in the same application.
- The life cycle of an ECP persistent volume is not independent of the owner application life cycle. Deleting an application or an application instance deletes the corresponding persistent volume(s) as well. This behavior is different from the native Kubernetes <span style="font-family: 'Courier New';">StatefulSet</span>

 Controller, where persistent volumes are not deleted when a <span style="font-family: 'Courier New';">StatefulSet</span>

 is deleted.

<!-- -->

### **Using <span style="font-family: 'Courier New';">local-ssd</span>

**

Specify a <span style="font-family: 'Courier New';">persistentVolumeClaim</span>

 (PVC) in <span style="font-family: 'Courier New';">volumeClaimTemplates</span>

 of a <span style="font-family: 'Courier New';">StatefulSet</span>

, set the <span style="font-family: 'Courier New';">storageClass</span>

 to <span style="font-family: 'Courier New';">local-ssd</span>

, and mount the PVC to your container.

```yaml
apiVersion: apps/v1
kind: StatefulSet
metadata:
  name: demoapp
  namespace: demo
spec:
  selector:
    matchLabels:
      app: demoapp
  template:
    metadata:
      labels:
        app: demoapp
    spec:
      containers:
      - image: nginx
        name: demoapp
        resources:
          limits:
            cpu: "200m"
            memory: 256Mi
          requests:
            cpu: "200m"
            memory: 256Mi
        volumeMounts:
        - mountPath: /tmp
          name: data
  volumeClaimTemplates:
  - metadata:
      annotations:
        volume.beta.kubernetes.io/storage-class: local-ssd
      name: data
    spec:
      accessModes:
      - ReadWriteOnce
      resources:
        requests:
          storage: 1G
```



### **Using <span style="font-family: 'Courier New';">persist-ssd</span>

**

Specify a <span style="font-family: 'Courier New';">persistentVolumeClaim</span>

 (PVC) in <span style="font-family: 'Courier New';">volumeClaimTemplates</span>

 of a <span style="font-family: 'Courier New';">StatefulSet</span>

, set the <span style="font-family: 'Courier New';">storageClass</span>

 to <span style="font-family: 'Courier New';">persist-ssd</span>

 and mount the PVC to your container.

```yaml
apiVersion: apps/v1
kind: StatefulSet
metadata:
  name: demoapp
  namespace: demo
spec:
  selector:
    matchLabels:
      app: demoapp
  template:
    metadata:
      labels:
        app: demoapp
    spec:
      containers:
      - image: nginx
        name: demoapp
        resources:
          limits:
            cpu: "200m"
            memory: 256Mi
          requests:
            cpu: "200m"
            memory: 256Mi
        volumeMounts:
        - mountPath: /tmp
          name: data
  volumeClaimTemplates:
  - metadata:
      annotations:
        volume.beta.kubernetes.io/storage-class: persist-ssd
      name: data
    spec:
      accessModes:
      - ReadWriteOnce
      resources:
        requests:
          storage: 1G
```

