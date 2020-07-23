# Configuring Applications

The first step in deploying your application to ECP clusters is to use the ECP-defined “Application” object. An ECP “Application” typically consists of a target, a Kubernetes workload controller, and a Layer 4 load balancer.

### Target

The target specifies where you want to run your application and the number of instances expected. Two target options are supported. The first option allows you to pick ECP locations that best fit your requirements by using the type `Location`. Alternatively, if you want to distribute your application within a region and want the ECP to pick locations automatically for you, use the type `RegionPreference`.
The following examples show how to configure different types of targets.

## Target of type “Location”

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

## Target of type “RegionPreference”

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

To expose your application, we recommend you use a Layer 4 load balancer as a frontend for your pods, unless there are special requirements to expose the pods directly. Unlike native Kubernetes, which defines a Service object for service discovery and load balancing of an application, the ECP offers a self-defined `LoadBalancer4` object to help you expose your application and load balance traffic. For more information, click [here](<#using-layer-4-load-balancing>).

## Sample Demo Configuration

The following example shows a demo configuration of an ECP application. In this example, the application will be deployed to two ECP locations, with some instances using the `Location` object. This example uses a `StatefulSet`
controller to declare that a container running NGINX web server will be spun up, with some compute/storage resources provisioned. It also exposes the NGINX containers and defines traffic-forwarding rules using the `LoadBalancer4` object.

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
- An “application name” parameter is required when an application configuration is to be deployed. The value of this parameter is used to fill the `metadata.name` fields of the target, workload controller, and `LoadBalancer4` objects. If you specify these `metadata.name` fields in the application configuration, make sure the values are consistent with the “application name” parameter.
- The target type must be either `Location` or `RegionPreference`. Mixed usage of the two types is not allowed. Because some ECP locations/regions might not be enabled for you, contact CDNetworks' sales engineers if you want to enable certain locations or regions, or if you have trouble deploying your application to ECP locations/regions.
- Not all Kubernetes workload Controllers are supported. We recommend you use a [StatefulSet](<https://kubernetes.io/docs/concepts/workloads/controllers/statefulset/>) Controller to run applications that require persistent storage. Otherwise, use a [ReplicaSet](<https://kubernetes.io/docs/concepts/workloads/controllers/replicaset/>) Controller.
- When configuring a workload Controller, leave the `spec.replicas` field empty because the equivalent is configured in the target object.
- If you need persistent volumes for your application, you can use two storage classes: `local-ssd` and `persist-ssd`. For more information, see [Using Storage Resources](<#using-storage-resources>).
- Running containers in privileged mode is not allowed.
