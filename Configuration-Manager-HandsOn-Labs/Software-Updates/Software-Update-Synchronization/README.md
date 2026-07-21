# Software Update Configuration and Deployment

### Selecting a Product for Software Updates

Go to **Administration** > **Sites** > right click **Configure Site Components** > **Software Update Point**

![SUS1](./images/SUP1.PNG)

Go to _Products Tab_ and select _Windows 10_

![SUS2](./images/SUP2.PNG)

Go to **Software Libary** > **All Software Updates** > **Synchronize Software Updates**

![SUS3](./images/SUP3.PNG)

### Check the Log Files for the status

Go to C:\Program Files\Microsoft Configuration Manager Logs

- **WCM.log** : used for troubleshooting Software Update Point (SUP) issues

![SUS4](./images/SUP4.PNG)

- **wsyncmgr.log** (WSUS Synchronization Manager log): the primary server-side log for tracking the synchronization process of software updates

![SUS5](./images/SUP5.PNG)

![SUS6](./images/SUP6.PNG)
