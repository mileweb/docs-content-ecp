# Managing CNAMEs 

After you deploy a containerized application to ECP edge locations across the globe, consider global traffic management, i.e. traffic routing. As an edge compute solution, the ECP platform helps on both edge application delivery and traffic management (using in-house DNS-based GSLB).

Prerequisites to enable the traffic routing feature:

- Use [ECP defined layer 4 load balancers](</docs/portal/applications/using-advanced-ecp-features.md#using-layer-4-load-balancing>) to expose your application instances.
- Create an ECP CNAME for your application to allow the ECP to manage traffic routing for the application.
- Point the DNS record of your application’s domain name to the ECP CNAME you created.

With the traffic routing feature enabled, incoming traffic to your application is routed automatically to optimal edge ECP locations where your application is running.

### CNAME Page

CNAMEs are managed from the CNAMEs page. To display this page, click **CNAMEs** in the left pane.

The following figure shows the key elements on the page, and the table following the figure describes them.

<p align=center><img src="/docs/resources/images/cnames/cnames-w-numbers.png" width="700"></p>

| **Fields**   | **Description**                                                                           |
| :----------: | ----------------------------------------------------------------------------------------- |
| 1            | To filter CNAMEs, type characters in this field and then press the Enter key. All CNAMEs that do not contain the typed characters are hidden. Filtering is not case-sensitive. To remove the filter, click the **Reset** button.                                   |
| 2            | Each CNAME appears on its own row. Clicking a CNAME allows you to view more [information](</docs/portal/cnames/viewing-cname-information.md>) about the CNAME. Clicking an application allows you to view information about the application associated with the CNAME.        |
| 3            | The **Actions** drop-down list on each row has options to [update](</docs/portal/cnames/updating-a-cname.md>) or [delete](</docs/portal/cnames/deleting-a-cname.md>) a CNAME.                                                                             |
| 4            | The **+ Add New CNAME** button allows you to [create](</docs/portal/cnames/adding-a-cname.md>) CNAMEs.    |