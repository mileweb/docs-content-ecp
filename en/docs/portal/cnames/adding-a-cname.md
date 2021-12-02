# Creating a CNAME

1. In the left pane, click **CNAMEs**.
2. At the top right of the CNAMEs page, click the **\+ Add New CNAME** button. 
3. Complete the fields in the Add CNAME form. Required fields are denoted by an asterisk (\*).

<p align=center><img src="/docs/resources/images/cnames/cnames-add-cname.png" width="600"></p>

| **Field**              | **Description**                                 |
| -----------------------|-------------------------------------------------| 
| CNAME                  | Either enter a CNAME prefix manually in the text field or click the **Auto Generate** button to have the ECP generate a CNAME prefix for you. If you enter a CNAME prefix, your typed entry must be a valid domain name label.    |
| Application            | Select an application you want to associate with this CNAME.                                                                |
| Description            | Enter a description for this CNAME.                                                                     |

4. Click the **Submit** button.

**Note:** You can create a CNAME for an application only when the application is exposed via ECP defined layer 4 load balancers. This is true across the lifecycle of an application. It means, if an application is initially deployed with ECP layer 4 load balancers as exposure method, but is later updated to remove the load balancers, any CNAME created for the application will need to be deleted before the application update can be accepted.