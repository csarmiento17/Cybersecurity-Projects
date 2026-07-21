# Deploy an Application using Package Deployment


### Pre-requisites

- Download an application (e.g Mozilla Firefox)
- Create a folder under **Software Library** > **Applications** > **Firefox**
- Make sure **Everyone** has access to the **Applications** Folder

### Create Package in Configuration Manager

Go to **Software Library** > **Application Management** > **Packages** > **Create Package**

![PackageDeployment1](./images/PackageDeployment1.PNG)

![PackageDeployment2](./images/PackageDeployment2.PNG)

![PackageDeployment3](./images/PackageDeployment3.PNG)

![PackageDeployment4](./images/PackageDeployment4.PNG)

![PackageDeployment5](./images/PackageDeployment5.PNG)

```
msiexec.exe /i "Firefox Setup 152.0.6.msi /q
```

![PackageDeployment6](./images/PackageDeployment6.PNG)

![PackageDeployment7](./images/PackageDeployment7.PNG)

![PackageDeployment8](./images/PackageDeployment8.PNG)


### Create Program for Uninstallation of Firefox

![PackageDeployment9](./images/PackageDeployment9.PNG)

![PackageDeployment10](./images/PackageDeployment10.PNG)

```
msiexec.exe /x "Firefox Setup 152.0.6.msi /q
```

![PackageDeployment11](./images/PackageDeployment11.PNG)

Click Next until you see the *Completion Window* then click Close

![PackageDeployment12](./images/PackageDeployment12.PNG)

### Distribute Content 

Note: You may follow this [example](https://github.com/csarmiento17/Cybersecurity-Projects/tree/master/Configuration-Manager-HandsOn-Labs/Software-Deployment/Deploy-In-Available-Mode) for step-by-step process on how to Distribute Content


###  Deploy to Client Computers

![PackageDeployment13](./images/PackageDeployment13.PNG)

![PackageDeployment14](./images/PackageDeployment14.PNG)

![PackageDeployment15](./images/PackageDeployment15.PNG)

![PackageDeployment16](./images/PackageDeployment16.PNG)

![PackageDeployment17](./images/PackageDeployment17.PNG)

![PackageDeployment18](./images/PackageDeployment18.PNG)

![PackageDeployment19](./images/PackageDeployment19.PNG)

![PackageDeployment20](./images/PackageDeployment20.PNG)

![PackageDeployment21](./images/PackageDeployment21.PNG)

![PackageDeployment22](./images/PackageDeployment22.PNG)

![PackageDeployment23](./images/PackageDeployment23.PNG)

![PackageDeployment24](./images/PackageDeployment24.PNG)

### Verify Client Computers

Location of the file that was downloaded locally

![PackageDeployment25](./images/PackageDeployment25.PNG)

![PackageDeployment26](./images/PackageDeployment26.PNG)
