# Reports

The ECP allows you to generate reports covering bandwidth, traffic, CPU, memory, storage, and pods and public IP addresses. The metrics related to CPU, memory, and storage are reported according to your resource requests rather than real-time consumption.

You can query reports for up to one year (366 days, which includes Leap Day). The report granularity can be as high as 1-minute or from medium to low, such as 5-minute, hourly, daily, and monthly. You can even query reports on applications that run in different ECP service zones.

If you are a reseller with child accounts, you can select the accounts that a report will cover (the parent account only, the child account only, or both the parent and child accounts).

## Reports Page

Reports are generated from the Reports page. To display this page, click **Reports** in the left pane.

The following figure shows the key elements on the page.

![null](</docs/resources/images/reports/reports-w-numbers.png>)

| **Element Number**       | **Description**                               |
| -------------------------|-----------------------------------------------| 
| 1                        | Specify the report type, date range, report interval, and service zone. Resellers with child accounts can also select a report range.                                                              |
| 2                        | The **Generate Report** button allows you to generate the report defined by the report parameters.                      |


# Understanding Report Types

The ECP supports the following type of reports. You select a report type from the **Report Type** drop-down list on the Reports page.

![null](</docs/resources/images/reports/reports-dropdown.png>)

| **Report**               | **Description**                               |
| -------------------------|-----------------------------------------------| 
| Bandwidth                | Shows the total peak incoming and outgoing bandwidth, peak total bandwidth, average total bandwidth (in bps), and how the values change over time.                                               |
| Traffic                  | Shows the total amount of incoming and outgoing traffic, the total traffic value (in bytes), and how the values change over time.                                                                      |
| CPU                      | Shows the peak CPU usage and how the value changes over time.         |
| Memory                   | Shows the peak memory usage and how the value changes over time.                                                         |
| Storage                  | Shows the peak local storage usage and peak persist storage usage (in bytes), and how the values change over time.     |
| Pods & Public IPs        | Shows the peak pod usage and peak IP usage, and how the values change over time.                                           |

# Generating Reports

1. In the left pane, click **Reports**. 
2. Complete the fields in the Reports form. Required fields are denoted by an asterisk (\*).

![null](</docs/resources/images/reports/reports-wo-numbers.png>)

| **Fields**               | **Description**                               |
| -------------------------|-----------------------------------------------| 
| Report Type              | Select the [type of report](<#understanding-report-types>) you want to generate.                      |
| Date Range               | Select the month, or a start date, end date, and time span for the report. If you select a start date, end date, and time span, use the **UTC** drop-down list to select a time zone.                |
| Report Interval          | Select the granularity of the returned data. Choices are:<ul><li><strong>1 Minute</strong> = this interval is supported when the time span does not exceed 7 days.</li><li><strong>5 Minutes</strong> = this interval is supported when the time span does not exceed 31 days.</li><li><strong>1 Hour</strong>.</li><li><strong>1 Day</strong>.<li><strong>1 Month</strong>.</li></ul>Raw report data is generated per 1 minute. The raw data is aggregated to provide reports of different granularities. The aggregation method is the “sum” for the metrics "inboundTraffic," "outboundTraffic," and "totalTraffic." For all other metrics, the aggregation method is "average."                              |
| Service Zone             | Select one or more service zone options. <ul><li><strong>Standard</strong> = standard service zone.</li><li><strong>Business</strong> = business service zone. (*default*).</li><li><strong>Premium</strong> = premium service zone.                                                                       |
| Report Range             | If you are a reseller with child accounts, select the accounts that this report will cover. Choices are:<ul><li><strong>This Account Only</strong>.</li><li><strong>Children Accounts Only</strong>.</li><li><strong>This Account + Children</strong>. (*default*)</li></li></ul>                                                                              |

3. Click the **Generate Report** button to generate the report.
4. With a generated report (similar to the one below) displayed at the bottom of the form, you can:

- Hold your cursor over data points in the report to view detailed information.
- Use the icons at the right side of the report to view regions, zoom, and reset magnification.
- Use the **Download** button at the top-right of the report to download the report in JPEG, PNG, and PDF formats.

![null](</docs/resources/images/reports/reports-generated-report.png>)