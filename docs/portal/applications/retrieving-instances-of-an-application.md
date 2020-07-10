# Retrieving Instances of an Application in List View

1. In the left pane, click **Applications**.
2. On the Applications page, click a link below the **Instances** column. A page similar to the following shows a list view of instance information for the selected application. The table below the figure describes the elements on this page.

![null](</docs/resources/images/applications/applications-instances-w-numbers.png>)

| **Element Number**       | **Description**                               |
| -------------------------|-----------------------------------------------| 
| 1                        | By default all PoPs for all phases are shown. Use the PoP and Phase drop-down lists to view a particular PoP and phase. The two right buttons reset the filters and refresh the instances shown.                                                                      |
| 2                        | Click an ID to view information about an   instance.                                                                   |
| 3                        | The **Actions** drop-down list on each row has options for viewing metrics, logs, and shell for an instance.               |
| 4                        | Use these buttons to go to other Instances pages.                                                                      |
|5                         | Use these icons to toggle between list view (which is the default) or map.                                              |
|6                         | Click this button to return to the Applications page.                                                                       |


# Retrieving Instances of an Application in Map View

1. In the left pane, click **Applications**.
2. On the Applications page, click a link below the **Instances** column. 
3. At the top right of the Instances page, click the <span><img src="/docs/resources/images/applications/applications-globe-icon.png" alt="globe" width="30"></span> icon.

![null](</docs/resources/images/applications/applications-instances.png>)

A map view similar to the following shows the location of the instances and their phases.

![null](</docs/resources/images/applications/applications-instances-map-view.png>)

4. By default, the map shows all PoPs and all phases. Using the **PoP** and **Phase** drop-down lists above the map, you can view a particular PoP and phase. The two right buttons next to the drop-down lists reset the filters and refresh the instances shown.
5. Clicking an Instance displays a popup similar to the following figure with detailed information. Clicking the link next to **Instance** displays detailed information about that instance, with buttons for viewing metrics, viewing and downloading logs, and running commands inside containers. For an example, see the figure under [Viewing Instance Information](<#viewing-instance-information>) below.

![null](</docs/resources/images/applications/applications-instances-map-view-detail.png>)

6. To return to the Applications page, click the **< Back** button at the top right.

# Viewing Instance Information

The following procedure describes how to view information about application instances.

1. In the left pane, click **Applications**.
2. On the Applications page, click the instance whose information you want to view. 
3. On the Instances page, click a link below the **ID** column. A form similar to the following appears. The table below the figure describes the elements on this form.

![null](</docs/resources/images/applications/applications-instance-details-basic-info-w-numbers.png>)

![null](</docs/resources/images/applications/applications-instance-details-conditions.png>)

![null](</docs/resources/images/applications/applications-instance-details-events.png>)

![null](</docs/resources/images/applications/applications-instance-details-containers.png>)

| **Element Number**       | **Description**                               |
| -------------------------|-----------------------------------------------| 
| 1                        | Click this button to return to the Instances page.                                                                      |
|2                         | Click this button to view metrics such as CPU, memory, traffic, and bandwidth usage in a popup. Controls at the top of the popup allow you to select metrics, interval, date and time, and UTC.                                                                        |
| 3                        | Click this button to obtain a live stream of logs from the instance.                                                     |
| 4                        | Click this button to run commands inside the instance.                                                                   |