# Using Advanced ECP Features

## Request Public IP Address for a Pod

When a pod gets created with the native Kubernetes, the pod is assigned a private IP address that is accessible only from within the Kubernetes cluster. CDNetworks’ ECP extensions to Kubernetes allow you to request a public IP address for a pod and support IPv4 and IPv6 protocols.

## Request Public IPv4 Address

To obtain a public IPv4 address for your pod, add an annotation to the pod spec. For example:

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

## Request Public IPv6 Address

To obtain a public IPv6 address for your pod, add an annotation to the pod spec. For example:

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

## Load Balancer Health Checks

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

The ECP platform defines the following storage class for different use cases of persistent storage:

- `local-ssd` is for local SSD storage. Data persists through container restarts and in-node recreations, but is lost when the pod is rescheduled to other nodes.

Observe the following guidelines:

- If persistent volumes are required, use `StatefulSet` Controller for your application.
- The requested capacity of a single `persistentVolumeClaim` (PVC) must be between 500MB and 100GB.
- The life cycle of an ECP persistent volume is not independent of the owner application life cycle. Deleting an application or an application instance deletes the corresponding persistent volume(s) as well. This behavior is different from the native Kubernetes `StatefulSet` Controller, where persistent volumes are not deleted when a `StatefulSet` is deleted.


## Using `local-ssd`

Specify a `persistentVolumeClaim` (PVC) in `volumeClaimTemplates` of a `StatefulSet`, set the `storageClass` to `local-ssd`, and mount the PVC to your container.

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





