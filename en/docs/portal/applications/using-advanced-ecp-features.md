# Using ECP Advanced Features

## Request Public IP Address for a Pod

When a pod gets created with the native Kubernetes, the pod is assigned a private IP address that is accessible only from within the Kubernetes cluster. ECP's extensions to Kubernetes allow you to request a public IP address for a pod, and both IPv4 and IPv6 protocols are supported.

### Request Public IPv4 Address

To obtain a public IPv4 address for your pod, add an annotation to the pod spec. For example:

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: myapp
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
```

### Request Public IPv6 Address

To obtain a public IPv6 address for your pod, add an annotation to the pod spec. For example:

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: myapp
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
```

## Use ECP defined Layer 4 Load Balancing

To expose your application, i.e. your pods running in an ECP Kubernetes cluster, the ECP defined layer 4 load balancer (also referred to as LB4) is recommended, unless it is required to expose the pods directly. Each ECP layer 4 load balancer is assigned a public IP address. It captures incoming traffic hitting its IP address, makes load balancing decision based on specified algorithm, and then forwards the traffic to backend pods that sit behind the load balancer. Refer to the following example.

```yaml
apiVersion: v1
kind: LoadBalancer4 # ECP defined layer 4 load balancer.
metadata:
  name: demo-lb4 
spec: 
  listeners:
  - backendPort: 80 # port of backend pods to receive forwarded traffic
    backendSelector: # select backend pods based on pod labels
      app: demoapp
    healthCheck: false # turn on/off health check. Set to false by default.
    listenerPort: 80 # port exposed by the layer 4 load balancer. Must be the same as “backendPort”.
    name: listener-80
    protocol: tcp # can be “tcp” or “udp”
    scheduler: lc # scheduling policy. Can be “lc”, “rr”, or "sh". Set to “lc” by default
```

### Layer 4 Load Balancer Health Checks

You can configure your layer 4 load balancer to run periodic health checks against the backend pods that sit behind it. Backend pods that fail such health checks will be skipped by the load balancer when forwarding traffic. TCP and HTTP health checks are supported.

**TCP Health Check**

```yaml
apiVersion: v1
kind: LoadBalancer4
metadata:
  name: demo-lb4 
spec: 
  listeners:
  - backendPort: 80
    backendSelector:
      app: demoapp
    healthCheck: true
    healthCheckType: tcp # can be “tcp” or “http”. “tcp” by default.
    healthCheckConnectPort: 80 # same as backendPort by default
    healthCheckInterval: 1 # 1 by default. Scope: 1-5  in seconds
    listenerPort: 80
    name: listener-80
    protocol: tcp
    scheduler: lc
```


**HTTP Health Check**

```yaml
apiVersion: v1
kind: LoadBalancer4
metadata:
  name: demo-lb4
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
    healthCheckInterval: 1 # 1 by default. Scope: 1-5  in seconds
    listenerPort: 80
    name: listener-80
    protocol: tcp
    scheduler: lc
```

## Use Storage Resources

The ECP platform defines the following storage class to provision persistent storage:

- `local-ssd` stands for local SSD storage. Data stored in it persists through container restarts and in-node recreations, but is lost when the pod is rescheduled to other nodes.

Observe the following guidelines:

- Use `StatefulSet` Controller for your application, if persistent volumes are required.
- The requested capacity of a single persistent volume must be between 500MB and 100GB.
- The lifecycle of an ECP persistent volume is NOT independent of the owner application. **Deleting an application or an application instance deletes the corresponding persistent volume(s) as well.** This behavior is different from the native Kubernetes `StatefulSet` Controller, where persistent volumes are not deleted when a `StatefulSet` is deleted.

**Note:** The disks backing a `local-ssd` volume are physically attached to the same machine that runs your containers. As such a volume is available locally on same machine as containers, the readwrite performance is optimal. However, there is no guarante of availability. In events of disk damage, machine crash or PoP outage, the storage will be lost or become inaccessible. Therefore, ECP `local-ssd` storage resource shall NOT be used for use cases that require high availability and reliability, e.g. database store.

### Use `local-ssd` storage

Specify a `persistentVolumeClaim` (PVC) in `volumeClaimTemplates` of a `StatefulSet`, set the `storageClass` to `local-ssd`, and mount the PVC to your container.

```yaml
apiVersion: apps/v1
kind: StatefulSet
metadata:
  name: demoapp
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
      - image: myapp
        name: demoapp
        resources:
          limits:
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
          storage: 10G
```





