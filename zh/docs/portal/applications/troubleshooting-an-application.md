# Troubleshooting an Application

Application inspection and debugging is an important part of application lifecycle management. The ECP portal has that covered. Check below the tools available.

## Events

Means [events](<https://kubernetes.io/docs/tasks/debug-application-cluster/events-stackdriver/>) that Kubernetes reports when deploying a pod and when the pod is running inside Kubernetes cluster. 

Go to the detail page of a specific application instance (i.e. a pod) and check events reported. You would find helpful debug info there, especially when the instance is stuck in a pending or failed state.

**Note:** The events are not persistent and are removed 3 hours after the last occurrence.

<p align=center><img src="/docs/resources/images/applications/applications-instance-details-events.png" width="600"></p>

## Logs Viewer

Go to the detail page of a specific application instance, click the top-right **Logs** button, and obtain a live stream of logs from your container. The output is the same as what you would see when you execute the `docker logs` command in your own Docker environment.

<p align=center><img src="/docs/resources/images/applications/applications-app-logs.png" width="600"></p>

## Cloud Shell

Go to the detail page of a specific application instance, click the top-right **Shell** button, and open a shell to your container to execute commands there inside. The effect is the same as executing the `docker exec` command in your own Docker environment.

<p align=center><img src="/docs/resources/images/applications/applications-app-shell.png" width="600"></p>

## Metrics

Go to the detail page of a specific application instance, click the top- right **Metrics** button, and retrieve metrics for the application instance, such as CPU and memory usage, traffic volume, and so on.
<p align=center><img src="/docs/resources/images/applications/applications-app-metrics.png" width="600"></p>
