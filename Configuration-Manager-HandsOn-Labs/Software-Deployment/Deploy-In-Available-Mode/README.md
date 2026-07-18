# Deploy Application in Available Mode

### Download 7zip App and Create Folders

Download 7zip installer

Go to **C:** and create Folders **Applications > 7zip**

![DeployApp1](./images/DeployApp1.PNG)

Copy the 7zip installer into 7zip folder

![DeployApp2](./images/DeployApp2.PNG)

Share the 7zip folder to Everyone

![DeployApp3](./images/DeployApp3.PNG)

Select the dropdown arrow and choose _Everyone_ then clic Add

![DeployApp4](./images/DeployApp4.PNG)

Change the Permission Level to Read/Write then click Share and Done

![DeployApp5](./images/DeployApp5.PNG)

### Create Application in MCM

Go to Microsoft Configuraiton Manager and Create an Application. Navigate to **Software Library** > right click **Applications** and select **Create Applicaiton**

![DeployApp6](./images/DeployApp6.PNG)

In **Location** put the network path of the installer then click Next. You can ignore the pop-up message if there's any.

![DeployApp7](./images/DeployApp7.PNG)

![DeployApp8](./images/DeployApp8.PNG)

Put the Publisher and Software Version. Click Next

![DeployApp9](./images/DeployApp9.PNG)

![DeployApp10](./images/DeployApp10.PNG)

![DeployApp11](./images/DeployApp11.PNG)

![DeployApp12](./images/DeployApp12.PNG)

### Distribute Content

Right click on the newly created 7zip Application and select _Distribute Content_

![DeployApp13](./images/DeployApp13.PNG)
![DeployApp14](./images/DeployApp14.PNG)
![DeployApp15](./images/DeployApp15.PNG)
![DeployApp16](./images/DeployApp16.PNG)
![DeployApp17](./images/DeployApp17.PNG)
![DeployApp18](./images/DeployApp18.PNG)
![DeployApp19](./images/DeployApp19.PNG)
![DeployApp20](./images/DeployApp20.PNG)
![DeployApp21](./images/DeployApp21.PNG)

### Deploy to Client Computers

![DeployApp22](./images/DeployApp22.PNG)

![DeployApp23](./images/DeployApp23.PNG)

Choose _Device Collection_ > _Windows 10 Devices_

![DeployApp24](./images/DeployApp24.PNG)
![DeployApp25](./images/DeployApp25.PNG)
![DeployApp26](./images/DeployApp26.PNG)

In Purpose choose _Available_ so users have the option to install it themself. Click Next

![DeployApp27](./images/DeployApp27.PNG)
![DeployApp28](./images/DeployApp28.PNG)
![DeployApp29](./images/DeployApp29.PNG)

If 50% of the deployment failed, it will create an alert. Click Next

![DeployApp30](./images/DeployApp30.PNG)
![DeployApp31](./images/DeployApp31.PNG)
![DeployApp32](./images/DeployApp32.PNG)

### Go to Software Center of the Client Computer

Go to **Software Center** to check if the 7zip application is available

![DeployApp33](./images/DeployApp33.PNG)
