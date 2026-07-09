# Configure Automatic Client Push Installation

The primary benefit of automatic client push installation in Microsoft Configuration Manager (formerly SCCM) is hands-free, automated endpoint onboarding. By integrating with Active Directory System Discovery, it dynamically detects new computers on your network and automatically pushes the client software, eliminating the need for manual deployment

### Configuration

You can see the Client column that we don't have a client at the moment.

![PushInstallation1](./images/PushInstallation1.PNG)

Go to Administration > Site Configuration > Sites

![PushInstallation2](./images/PushInstallation2.PNG)

Right click the Site, choose Client Installation Settings > Client Push Installation

![PushInstallation3](./images/PushInstallation3.PNG)

In _Client Push Installation Properties_ window select the following.

- Enable automatic side-wide client push installation
- Configuration Manager site system servers
- Always install the Configuration Manager client on domain controllers

![PushInstallation4](./images/PushInstallation4.PNG)

Go to _Accounts Tab_ and add an account with Domain Admin priviledge.

![PushInstallation5](./images/PushInstallation5.PNG)

Click Browse then enter the account and enter the password the click Verify

![PushInstallation6](./images/PushInstallation6.PNG)

In the Network Share, enter a path where the account has access to verify the connection. Click OK then Apply.

![PushInstallation7](./images/PushInstallation7.PNG)

### Push Client to all the Computers

Go to Assets and Compliance > Devices. Select the client you want to include, right click then select _Install Client_

![PushInstallation8](./images/PushInstallation8.PNG)

In _Before You Begin_ click Next

![PushInstallation9](./images/PushInstallation9.PNG)

Select Install the client software from a specified site. Click Next then Close

![PushInstallation10](./images/PushInstallation10.PNG)

Give it a couple of minutes for the agent to install in computers

![PushInstallation11](./images/PushInstallation11.PNG)
