# Discovery of Resrources From Active Directory to MECP Console

## Summary

### Enable Active Directory Forest

Go to Administration > Hierarchy Configuration > Discovery Methods. Right click _Active Directory Forest Directory_ and select Properties

![Discovery1](./images/Discovery1.PNG)

### Enable Active Directory Group Discovery

Go to Administration > Hierarchy Configuration > Discovery Methods. Right click _Active Directory Group Discovery_ and select Properties

In the _Add Active Directory Location_ window, add Name and click Browse and select _jayslab_ and click OK then Apply

![Discovery2](./images/Discovery2.PNG)

Go to Assets and Compliance > Users and check if the Groups are being discovered by MECM

![Discovery7](./images/Discovery7.PNG)

### Enable Active Directory System Discovery

Go to Administration > Hierarchy Configuration > Discovery Methods. Right click _Active Directory System Discovery_ and select Properties.

- Enable Active Directory System Discovery
- Click the Yellow icon in Active Directory containers

![Discovery3](./images/Discovery3.PNG)

Select Browse and choose the option _Computers_ and click OK. Do the same thing and choose the option _Domain Controllers_.

![Discovery4](./images/Discovery4.PNG)

Click _Apply_ and _OK_

Go to Assets and Compliance > Users and check if the computer systems are being discovered by MECM

![Discovery8](./images/Discovery8.PNG)

### Enable Active Directory User Discovery

Go to Administration > Hierarchy Configuration > Discovery Methods. Right click _Active Directory User Discovery_ and select Properties

- Enable Active Directory User Discovery
- Click the Yellow icon in Active Directory containers

![Discovery5](./images/Discovery5.PNG)

Select _Browse_ and choose _jayslab_ and click OK and Apply

![Discovery6](./images/Discovery6.PNG)

Go to Assets and Compliance > Users and check if the computer systems are being discovered by MECM

![Discovery](./images/Discovery.PNG)
