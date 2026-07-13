# Manage Client Settings

Control how the Configuration Manager client behaves on managed devices. It allows you to modify the Default Client Settings (applied to all computers in your hierarchy) or create Custom Client Settings that override the defaults for specific device or user collections.

### Create Custom Client Settings

Go to *Administration* > right click *Create Custom Client Device Settings*

![ClientSettings1](./images/ClientSettings1.PNG)

- Client Cache Settings

![ClientSettings2](./images/ClientSettings2.PNG)

- Client Policy

 Since we have few computers we will change it to a lower polling inverval

![ClientSettings3](./images/ClientSettings3.PNG)


-Computer Agent

Select *Bypass* so it will not look for digital signature and block the execution

![ClientSettings4](./images/ClientSettings4.PNG)

-Computer Restart

We're changing to a lower value for testing purposes

![ClientSettings5](./images/ClientSettings5.PNG)

-Hardware Inventory

![ClientSettings6](./images/ClientSettings6.PNG)
![ClientSettings7](./images/ClientSettings7.PNG)



-Remote Tools

![ClientSettings8](./images/ClientSettings8.PNG)

Select the account who has domain admin access

![ClientSettings9](./images/ClientSettings9.PNG)

-Software Center

![ClientSettings10](./images/ClientSettings10.PNG)

-Software Deployment

![ClientSettings11](./images/ClientSettings11.PNG)

-Software Inventory

Change to *1 Hour* and add .exe, .msi and .xml in *Set Types*

![ClientSettings12](./images/ClientSettings12.PNG)

![ClientSettings13](./images/ClientSettings13.PNG)

-Software Metering

![ClientSettings14](./images/ClientSettings14.PNG)

-Software Updates

Sofware update scan schedule: 1 Hour
Schedule deployment re-evaluation: 1 Hour
Enable manamgement of the Office 365 Client Agent: Yes

![ClientSettings15](./images/ClientSettings15.PNG)

-State Messaging

![ClientSettings16](./images/ClientSettings16.PNG)

-User and Device Affinity

![ClientSettings17](./images/ClientSettings17.PNG)

### Deploy to Client Machines

Right click the newly created custom client settings and choose *Deploy*
![ClientSettings18](./images/ClientSettings18.PNG)

Select *All Desktop and Server Clients*

![ClientSettings19](./images/ClientSettings19.PNG)
