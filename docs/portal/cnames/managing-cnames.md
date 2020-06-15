<!--?xml version="1.0" encoding="utf-8"?-->

<link href="../Resources/TableStyles/Rows.css" rel="stylesheet" madcap:stylesheettype="table">

# Managing CNAMEs 

After you deploy a containerized application and run it in ECP edge locations across the globe, consider global traffic management. As an edge compute solution, the ECP platform helps to deliver your application to the edge and routes end-user traffic for the application using CDNetworks' DNS-based GSLB.

To use the GSLB:

- Expose your application in each ECP location using a Layer 4 load balancer.
- Create a Canonical Name Record (CNAME) to allow the ECP to manage traffic routing for the application.
- Point the DNS record of your application’s domain to the CNAME you created.

<!-- -->

Any incoming traffic to your application is routed automatically to the edge locations where your application is running based on both proximity and serving capacity



### <u style="font-weight: normal;font-style: normal;font-variant: small-caps;text-decoration: none;"><span style="font-variant: normal;">CNAME&nbsp;Page</span></u>



CNAMEs are managed from the CNAME page. To display this page, click **CNAMEs** in the left pane.

The following figure shows the key elements on the page, and the table following the figure describes them.

![null](</docs/resources/images/cnames/CNAMES_Overview.png>)

<span style="color: #708090; font-size: 9pt;">(click to enlarge)</span>

|  |
|  |
|  |
|  |
|  |
|  |

