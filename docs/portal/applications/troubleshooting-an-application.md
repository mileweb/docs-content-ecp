<!--?xml version="1.0" encoding="utf-8"?-->

# Troubleshooting an Application

In addition to helping manage the life cycle of your containerized application, the Portal provides tools for troubleshooting your application.

## Events

Go to the detail page of a specific application instance and check [Kubernetes events](<https://kubernetes.io/docs/tasks/debug-application-cluster/events-stackdriver/>) for the instance to see the activities that are occurring.

**Note:** The events are not persistent and are removed 3 hours after the last occurrence.

![null](</docs/resources/images/applications/Troubleshooting - Events.png>)

<span style="color: #708090; font-size: 9pt;">(click to enlarge)</span>

## Log Viewer

Go to the detail page of a specific application instance, click the top right **Logs** button, and obtain a live stream of logs from your container. The output is the same as what you would see if you issue the <span style="font-family: 'Courier New';">docker logs</span>

 command in your own Docker environment.

![null](</docs/resources/images/applications/Troubleshooting - Log Viewer.png>)

<span style="color: #708090; font-size: 9pt;">(click to enlarge)</span>

## Cloud Shell

Go to the detail page of a specific application instance, click the top-right **Shell** button, and obtain a shell to your container to execute commands inside the container. The effect is the same as issuing the <span style="font-family: 'Courier New';">docker exec</span>

 command in your own Docker environment.

![null](</docs/resources/images/applications/Troubleshooting - Clous Shell.png>)

<span style="color: #708090; font-size: 9pt;">(click to enlarge)</span>

## Metrics

Go to the detail page of a specific application instance, click the top right **Metrics** button, and obtain metrics for the application instance, such as CPU and memory usage, traffic volume, and so on.

![null](</docs/resources/images/applications/Troubleshooting - Metrics.png>)

<span style="color: #708090; font-size: 9pt;">(click to enlarge)</span>

