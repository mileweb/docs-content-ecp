# Managing CNAMEs 

After you deploy a containerized application and run it in ECP edge locations across the globe, consider global traffic management. As an edge compute solution, the ECP platform helps to deliver your application to the edge and routes end-user traffic for the application using CDNetworks' DNS-based GSLB.

To use the GSLB:

- Expose your application in each ECP location using a Layer 4 load balancer.
- Create a Canonical Name Record (CNAME) to allow the ECP to manage traffic routing for the application.
- Point the DNS record of your application’s domain to the CNAME you created.

Any incoming traffic to your application is routed automatically to the edge locations where your application is running based on both proximity and serving capacity

### CNAME Page

CNAMEs are managed from the CNAME page. To display this page, click **CNAMEs** in the left pane.

The following figure shows the key elements on the page, and the table following the figure describes them.

<p align=center><img src="/docs/resources/images/cnames/cnames-w-numbers.png" width="700"></p>

| **Element Number**     | **Description**                                 |
| -----------------------|-------------------------------------------------| 
| 1                      | To filter CNAMEs, type characters in this field and then press the Enter key. All CNAMEs that do not contain the typed characters are hidden. Filtering is not case-sensitive. To remove the filter, click the **Reset** button.                                                                   |
| 2                      | Each CNAME appears on its own row. Clicking a CNAME allows you to view basic [information](</docs/portal/cnames/viewing-cname-information.md>) about the CNAME. Clicking a CNAME application allows you to view information about the application associated with the CNAME. |
| 3                      | The **Actions** drop-down list on each row has options to [update](</docs/portal/cnames/updating-a-cname.md>) or [delete](</docs/portal/cnames/deleting-a-cname.md>) a CNAME.                                                                    |
| 4                      | The **+ Add New CNAME** button allows you to [create](</docs/portal/cnames/adding-a-cname.md>) CNAMEs.                         |