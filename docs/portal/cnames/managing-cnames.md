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

![null](</docs/resources/images/cnames/cnames-w-numbers.png>)

*TO MARC: NEED TO PUT THE TABLE HERE. IT WASN'T CONVERTED PROPERLY*