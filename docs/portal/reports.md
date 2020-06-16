# Reports

The ECP allows you to generate reports covering bandwidth, traffic, CPU, memory, storage, and pods and public IP addresses. The metrics related to CPU, memory, and storage are reported according to your resource requests rather than real-time consumption.

You can query reports for up to one year (366 days, which includes Leap Day). The report granularity can be as high as 1-minute or from medium to low, such as 5-minute, hourly, daily, and monthly. You can even query reports on applications that run in different [ECP service zones](<Zones.htm>).

If you are a reseller with child accounts, you can select the accounts that a report will cover (the parent account only, the child account only, or both the parent and child accounts).

### **Reports page**

Reports are generated from the Reports page. To display this page, click **Reports** in the left pane.

The following figure shows the key elements on the page.

![null](</docs/resources/images/reports/reports-w-numbers.png>)

*TO MARC: NEED TO PUT THE TABLE HERE. IT WASN'T CONVERTED PROPERLY*

# Understanding Report Types

The ECP supports the following type of reports. You select a report type from the **Report Type** drop-down list on the Reports page.

![null](</docs/resources/images/reports/reports-dropdown.png>)

| **Report**                                                                                                                                         | **Description**                                                                                                                                    |
| -------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------- |
| Bandwidth                                                                                                                                          | Shows the total peak incoming and outgoing bandwidth, peak total bandwidth, average total bandwidth (in bps), and how the values change over time. |
| Traffic                                                                                                                                            | Shows the total amount of incoming and outgoing traffic, the total traffic value (in bytes), and how the values change over time.                  |
| CPU                                                                                                                                                | Shows the peak CPU usage and how the value changes over time.                                                                                      |
| Memory                                                                                                                                             | Shows the peak memory usage and how the value changes over time.                                                                                   |
| Storage                                                                                                                                            | Shows the peak local storage usage and peak persist storage usage (in bytes), and how the values change over time.                                 |
| Pods & Public IPs                                                                                                                                  | Shows the peak pod usage and peak IP usage, and how the values change over time.                                                                   |

# Generating Reports

1. In the left pane, click **Reports**. 
2. Complete the fields in the Reports form. Required fields are denoted by an asterisk (\*).

![null](</docs/resources/images/reports/reports-wo-numbers.png>)

| **Fields**                                                                                                                                                                            | **Description**                                                                                                                                                                       |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Report Type                                                                                                                                                                           | Select the [type of report](<Understanding Report Types.htm>) you want to generate.                                                                                                   |
| Date Range                                                                                                                                                                            | Select the month, or a start date, end date, and time span for the report. If you select a start date, end date, and time span, use the **UTC** drop-down list to select a time zone. |
| Report Interval                                                                                                                                                                       | Select the granularity of the returned data. Choices are:                                                                                                                             |
| Service Zone                                                                                                                                                                          | Select one or more [service zone](<Zones.htm>) options.                                                                                                                               |
| Report Range                                                                                                                                                                          | If you are a reseller with child accounts, select the accounts that this report will cover. Choices are:                                                                              |

1. Click the **Generate Report** button to generate the report.
2. With a generated report (similar to the one below) displayed at the bottom of the form, you can:

- Mouse over data points in the report to view detailed information.
- Use the icons at the right side of the report to view regions, zoom, and reset magnification.
- Use the **Download** button at the top-right of the report to download the report in JPEG, PNG, and PDF formats.

![null](</docs/resources/images/reports/reports-generated-report.png>)