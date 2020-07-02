# Creating a CNAME

You can create a CNAME for an application only when the application is exposed by an ECP Layer 4 load balancer. This is true across the life cycle of an application. For example, if an application is initially deployed with Layer 4 load balancers, but is later updated to remove the load balancers, the CNAME for the application will be deleted before the application update is accepted.

1. In the left pane, click **CNAMEs**.
2. At the top right of the CNAMEs page, click the **\+ Add New CNAME** button. 
3. Complete the fields in the Add CNAME form. Required fields are denoted by an asterisk (\*).

![null](</docs/resources/images/cnames/cnames-add-cname.png>)

| **Field**              | **Description**                                 |
| -----------------------|-------------------------------------------------| 
| CNAME                  | Either enter a CNAME prefix manually in the text field or click Auto Generate to have the ECP generate a CNAME for you. If you enter a CNAME prefix, your typed entry must be a valid domain name.    |
| Application            | Select an application you want to associate with this CNAME.                                                                |
| Description            | Enter a description for this CNAME.                                                                     |

4. Click the **Submit** button.