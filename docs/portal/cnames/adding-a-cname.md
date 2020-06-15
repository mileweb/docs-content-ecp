<!--?xml version="1.0" encoding="utf-8"?-->

<link href="../Resources/TableStyles/Rows.css" rel="stylesheet" madcap:stylesheettype="table">

# Creating a CNAME

You can create a CNAME for an application only when the application is exposed by an ECP Layer 4 load balancer. This is true across the life cycle of an application. For example, if an application is initially deployed with Layer 4 load balancers, but is later updated to remove the load balancers, the CNAME for the application will be deleted before the application update is accepted.

1. In the left pane, click **CNAMEs**.
2. At the top right of the CNAMEs page, click the **\+ Add New CNAME** button. 
3. Complete the fields in the Add CNAME form. Required fields are denoted by an asterisk (\*).

<!-- -->

![null](</docs/resources/images/cnames/cname1.png>)

<span style="color: #708090; font-size: 9pt;">(click to enlarge)</span>

| **Fields**                                                                                                                                                                                         | **Description**                                                                                                                                                                                    |
| -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| CNAME                                                                                                                                                                                              | Either enter a CNAME prefix manually in the text field or click Auto Generate to have the ECP generate a CNAME for you. If you enter a CNAME prefix, your typed entry must be a valid domain name. |
| Application                                                                                                                                                                                        | Select an application you want to associate with this CNAME.                                                                                                                                       |
| Description                                                                                                                                                                                        | Enter a description for this CNAME.                                                                                                                                                                |

1. Click the **Submit** button.

<!-- -->

