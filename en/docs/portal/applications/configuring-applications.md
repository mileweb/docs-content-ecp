# Configuring Applications

You can create an ECP application either by [following a step-by-step wizard](</docs/portal/applications/adding-and-deploying-applications-using-a-wizard.md>) or by [providing a file](</docs/portal/applications/adding-and-deploying-applications-using-an-existing-configuration-file.md>) that contains application configuration.

If you choose to create the application from a file, the first step is to prepare the file if it does not exist yet. The file should contain specifications of the following objects that typically make up an ECP application:<ul><li>A target</ul></li><ul><li>A Kubernetes workload controller</ul></li><ul><li>A layer 4 load balancer</ul></li>

### Target

A Target object specifies where you want to run your application and how many instances are desired. Two target options are supported. The first option allows you to pick ECP locations that best fit your requirements by using the type `Location`. Alternatively, if you want to distribute your application within an ECP Region and want the ECP to pick locations automatically for you, use the type `RegionPreference`. Refer to this [Global Presence page](</docs/portal/global-presence.md>) to see a list of ECP locations and how the locations are grouped into ECP Regions.

The following examples show how to configure different target types.

## Target of type “Location”

```yaml
apiVersion: v1
kind: Location # use ECP defined Location object to specify target locations and desired number of instances
metadata:
  name: demo
spec:
  locations:
  - name: mia # use ECP PoP code to specify an ECP location
    replicas: 1 # specify the number of instances to be deployed to an ECP location
  - name: icn
    replicas: 2
```

## Target of type “RegionPreference”

```yaml
apiVersion: v1
kind: RegionPreference # use ECP defined RegionPreference object to specify target regions and desired number of instances
metadata:
  name: demo
spec:
  regions:
  - name: NA-WEST # use ECP Region code to specify an ECP Region
    replicas: 8 # specify number of instances to be distributed across locations in an ECP Region
  - name: APAC
    replicas: 5
```

## Kubernetes Workload Controller

A Kubernetes workload controller controls the desired state of an application instance. It includes such specifications as container image, compute/storage resources request, container startup commands and args, etc. The workload controller is configured the same way as the [native Kubernetes Controller](<https://kubernetes.io/docs/concepts/workloads/controllers/deployment/>), except that the desired pod replicas are specified via a Target object.

## Layer 4 Load Balancer

To expose your application, we recommend you use ECP defined layer 4 load balancers (also referred to as LB4) as frontend for your application instances (i.e. Kubernetes pods), unless it is required to expose the pods directly. Each ECP layer 4 load balancer is assigned a public IP address. It captures incoming traffic hitting its IP address, makes load balancing decision based on specified algorithm, and then forwards the traffic to backend pods that sit behind the load balancer. For more about how to configure the ECP load balancer, click [here](</docs/portal/applications/using-ecp-advanced-features.md#use-ecp-defined-layer-4-load-balancing>).

## Sample Demo Configuration

The following example shows a demo configuration of an ECP application. In this example, the `Location` object specifies 2 target ECP locations. The `StatefulSet`
controller declares that a container running NGINX web server shall be started, with some compute/storage resources provisioned. The `LoadBalancer4` object is specified to expose the NGINX containers and to define traffic-forwarding rules.

```yaml
apiVersion: v1
kind: Location # specify target locations and desired number of instances
metadata:
  name: demo
spec:
  locations:
  - name: mia # use ECP PoP code to specify an ECP location
    replicas: 1 # number of instances to be deployed to an ECP location
  - name: icn
    replicas: 2
---
apiVersion: apps/v1
kind: StatefulSet # specify a Kubernetes workload controller. Can be StatefulSet or Deployment. Use StatefulSet if persistent storage is required.
metadata:
  name: demo
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
        volumeMounts: # mount a persistent volume to a container. Optional.
        - mountPath: /data
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
          storage: 10G
---
apiVersion: v1
kind: LoadBalancer4 # ECP defined layer 4 load balancer. Use this to expose your application.
metadata: 
  name: demo
spec: 
  listeners: # specify traffic forward rules
  - backendPort: 80 # port of backend pods that receive forwarded traffic
    backendSelector: # select pods that sit behind this layer 4 load balancer
      app: demoapp
    healthCheck: false 
    listenerPort: 80 # port that this layer 4 load balancer listens on
    name: listener-80
    protocol: tcp
    scheduler: lc

```

Observe the following guidelines:

- The ECP accepts application configurations in JSON or YAML format. Like Kubernetes, YAML is the preferred format.
- Wrap the composing objects of an ECP application into a single JSON or YAML file before submitting to the ECP. PATCHing an existing application allows submission of incomplete application configuration.
- An “Application Name” parameter is required when an application configuration is to be deployed. The value of this parameter is used to fill the `metadata.name` fields of the target, workload controller, and `LoadBalancer4` objects. If you specify these `metadata.name` fields in the application configuration, make sure the values are consistent with the “Application Name” parameter.
- The Target type must be either `Location` or `RegionPreference`. Mixed usage of the two types is not allowed. Some ECP locations or Regions might not have been enabled for your account. Contact our sales engineers if you want to use certain locations or Regions, or if you have trouble deploying your application to ECP locations or Regions.
- Not all Kubernetes workload Controllers are supported. We recommend you use a [StatefulSet](<https://kubernetes.io/docs/concepts/workloads/controllers/statefulset/>) Controller to run applications that require persistent storage. Otherwise, use a [Deployment](<https://kubernetes.io/docs/concepts/workloads/controllers/deployment/>).
- When configuring a workload Controller, leave the `spec.replicas` field empty because the equivalent is configured in the Target object.
- If you need persistent volumes for your application, you can use the storage class `local-ssd`. For more information, see [Using Storage Resources](</docs/portal/applications/using-ecp-advanced-features.md#use-storage-resources>).
- Running containers in privileged mode is NOT allowed.
