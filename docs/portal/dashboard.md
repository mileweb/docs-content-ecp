# Understanding the Dashboard

The Dashboard is the landing page after you log in to the ECP. It provides an overview of resource quota consumption and resource usage metrics.

When you subscribe to the ECP, restrictions are enforced on the total amount of resources available to you across all PoPs in the ECP platform. These restrictions (called “resource quotas”) ensure that resource consumption does not exceed the quotas. Resource quotas are consumed by your containerized applications. All resource requests are checked against the resource quotas. If any incoming resource request will cause the cumulative resource quota consumption to be exceeded, the request will be rejected.

Within the ECP platform, high-level types of resources include compute, storage, and network. The Dashboard provides an overview of how your applications are using these resources.

Resource quota charts at the top of the Dashboard show “quota consumed” and “quota available” percentages for quotas in CPU, memory, and public IPv4 addresses. In the backend, additional quotas are imposed, including:

- Number of applications
- Number of pods
- Capacity of local-SSD storage
- Capacity of persist-SSD storage

![null](</docs/resources/images/dashboard/dashboard-resource-quota.png>)

Charts at the bottom of the Dashboard show usage metrics. Buttons above the usage metrics charts allow you to filter the metrics by the last 24 hours (the default view), last 7 days, or last month. A legend below the usage metrics charts shows the names of the data entry points in the chart. Clicking a data entry point name in the legend removes that data entry point from the chart. Clicking it again redisplays the data entry point. Clicking **View Full Report** below a usage metrics chart displays that chart on the [Reports page](</docs/portal/reports.md>), where you can define report parameters, and then view the results on the selected chart.

![null](</docs/resources/images/dashboard/dashboard-metrics-cpu.png>)

![null](</docs/resources/images/dashboard/dashboard-metrics-memory.png>)

![null](</docs/resources/images/dashboard/dashboard-metrics-traffic.png>)

![null](</docs/resources/images/dashboard/dashboard-metrics-bandwidth.png>)

![null](</docs/resources/images/dashboard/dashboard-metrics-storage.png>)

![null](</docs/resources/images/dashboard/dashboard-metrics-pods-and-ips.png>)


Hovering your cursor over the data points in a resource quota or usage metrics chart displays detailed information. For example:

![null](</docs/resources/images/dashboard/dashboard-resource-quota-hovered.png>)

![null](</docs/resources/images/dashboard/dashboard-metrics-pods-and-ips-hovered.png>)

The metrics related to CPU, memory, and storage are reported according to your resource requests for your applications. These metrics do not refer to real-time resource consumption by the processes running in your applications. For instance, if you request 1 vCPU core for your application when only 0.5 core is being used, the CPU metric value shown on the Dashboard will be the 1 vCPU core.

If you find on the portal or through an API call that high resource consumption is causing resource requests to be rejected, contact CDNetworks' sales engineers to adjust the quotas for you. You will not incur higher costs by setting higher quotas. Billing is based on resources requested and allocated for your applications.

