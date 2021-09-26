# Troubleshooting an Application

In addition to helping manage the life cycle of your containerized application, the portal provides tools for troubleshooting your application.

## Events

Go to the detail page of a specific application instance and check [Kubernetes events](<https://kubernetes.io/docs/tasks/debug-application-cluster/events-stackdriver/>) for the instance to see the activities that are occurring.

**Note:** The events are not persistent and are removed 3 hours after the last occurrence.

<p align=center><img src="/docs/resources/images/applications/applications-instance-details-events.png" width="600"></p>

## Log Viewer

Go to the detail page of a specific application instance, click the top-right **Logs** button, and obtain a live stream of logs from your container. The output is the same as what you would see if you issue the `docker logs` command in your own Docker environment.

<p align=center><img src="/docs/resources/images/applications/applications-app-logs.png" width="600"></p>

## Cloud Shell

Go to the detail page of a specific application instance, click the top-right **Shell** button, and obtain a shell to your container to execute commands inside the container. The effect is the same as issuing the `docker exec` command in your own Docker environment.

<p align=center><img src="/docs/resources/images/applications/applications-app-shell.png" width="600"></p>

## Metrics

Go to the detail page of a specific application instance, click the top- right **Metrics** button, and obtain metrics for the application instance, such as CPU and memory usage, traffic volume, and so on.
<p align=center><img src="/docs/resources/images/applications/applications-app-metrics.png" width="600"></p>
