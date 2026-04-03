# Active Directory Home Lab with Splunk & Attack Simulation

## Summary

This project demonstrates the setup of a fully functional cybersecurity home lab designed to simulate real-world attack scenarios and analyze generated telemetry.

The lab environment includes an Active Directory domain built on Windows Server 2022, a Windows 10 endpoint, and a Splunk SIEM instance deployed on an Ubuntu Server for centralized log collection. Logs are ingested from both the Domain Controller and the target machine (Windows 10) to provide visibility into system and security events.

To simulate adversarial activity, Kali Linux is used to perform a brute-force attack against the environment using Hydra.

This project also provides setting up of some of the environment in VirtualBox, including the installation and configuration of systems and tools.

Key Objectives:

- Build and configure an Active Directory lab environment
- Centralize log collection using Splunk
- Simulate brute-force attacks and adversary techniques
- Gain hands-on experience with red team concepts

**Not Included in this document but _required_:**

- Setting up of NAT Networks are not shown in this document, you may research on how to implement that.
- Configuring the Virtual Machines to use the NAT Network you created so they are on the same network and have intenet connectivity
- Creating of Shared Folders from Ubuntu to map the Splunk installer
- Adding of users to group **_vboxsf_**

### Diagram

![Active Directory Home Lab Diagram](./images/Diagram.PNG)

### Tools

| Application         | Description                        | Download link                                                                           |
| ------------------- | ---------------------------------- | --------------------------------------------------------------------------------------- |
| Windows 10          | Target machine                     | [Click here](https://www.microsoft.com/en-ca/software-download/windows10)               |
| Windows Server 2022 | Domain Controller                  | [Click here](https://www.microsoft.com/en-us/evalcenter/download-windows-server-2022)   |
| Ubuntu              | Splunk Server                      | [Click here](https://ubuntu.com/download/server)                                        |
| Splunk              | SIEM of choice                     | [Click here](https://www.splunk.com/en_us/download/splunk-enterprise.html?locale=en_us) |
| Kali Linux          | Attacker's machine                 | [Click here](https://www.kali.org/get-kali/#kali-virtual-machines)                      |
| 7-zip               | To extract the Kali Linux VM       | [Click here](https://www.7-zip.org/)                                                    |
| Sysmon              | To monitor and log system activity | [Click here](https://learn.microsoft.com/en-us/sysinternals/downloads/sysmon)           |

### Installation

**_Windows 10:_**

- While downloading, select the following options in the pop-up window:
  - Create installation media
  - ISO file
- While installing, select the following options in the pop-up window:
  - I don't have a product key
  - Windows 10 Pro
  - Custom: Install Windows only (advanced)

![Windows 10 Installation](./images/Win10.PNG)

**_Kali Linux:_**

- I suggest to just download the pre-built virtual machine, check if you have a 32-bit or 64-bit machine so you know what to download
- You also need to download and install 7-zip to extract the Kali Linux VM
- After you extract the downloaded Kali VM, double click the **_.vbox_** file extension and it will automatically be imported to VirtualBox
- Default credentials for Kali Linux is **_kali/kali_**

**_Windows Server 2022:_**

- Click on the **New** icon in VirtualBox, enter a Name, and select the **ISO** file you downloaded
- Select **Skip Unattended Installation**
- Select **Windows Server 2022 Standard Evaluation (Desktop Experience)**

![WinServer 2022](./images/WinSvr2022.PNG)

Promote **Active Directory** to **Domain Controller** by following
the screenshots below:

![ADDS](./images/ADDS1.PNG)
![ADDS](./images/ADDS2.PNG)
![ADDS](./images/ADDS3.PNG)
![ADDS](./images/ADDS4.PNG)
![ADDS](./images/ADDS5.PNG)
![ADDS](./images/ADDS6.PNG)
![ADDS](./images/ADDS7.PNG)
![ADDS](./images/ADDS8.PNG)

- OUs (Organizational Units) and Users have been created but are not shown in the screenshots. Please ensure you create them as well, as they will be used when joining the Windows 10 machine to the domain.

**_Ubuntu Server_**

- Similar to how you install the Windows Server 2022, click on the **New** icon in VirtualBox, enter a Name, and select the **ISO** file you downloaded
- While installing, select the following options in the screen:
  - Try or Install Ubuntu Server
  - Continue without updating
  - In **Mirror check still running** screen, select **Continue**

  ![Credentials Info](./images/UbuntuSvr2.PNG)
  - Select **Continue** or **Done** until the setup starts installing
  - Select **Reboot Now** when it appears
  - Run the Update and Upgrade command
    - `sudo apt-get update && sudo apt-get upgrade -y`

- Create a static IP address (I'm using version 24, if you are using version 22 you might have different file e.g. **_00-installer-config.yaml_**)
- Add a DNS and Default Route
- Verify that the IP address has changed

![StaticIP](./images/Splunk_StaticIP.PNG)

![StaticIP](./images/Splunk_StaticIP_2.PNG)

![StaticIP](./images/Splunk_StaticIP_3.PNG)

**_Splunk_**

- Download Splunk Enterprise, select the Linux (.deb file)
- Install the highlighted packages add-ons for VirtualBox

![VirtualBoxAddons](./images/Splunk4.PNG)

- Install Splunk

![VirtualBoxAddons](./images/Splunk5.PNG)

- Change into the directory where Splunk is located into the server

![VirtualBoxAddons](./images/Splunk6.PNG)

- Change into the user **_splunk_** using the below command
  - `sudo -u splunk bash`
- Change into **_bin_** directory and start the installation of Splunk
  - `cd bin`
  - `./splunk start`

- Run the commands below to ensure Splunk starts whenever the server reboots
  - `exit`
  - `cd bin`
  - `sudo ./splunk enable boot-start -user splunk`

![VirtualBoxAddons](./images/Splunk7.PNG)

**_Installing Splunk Universal Forwarder in Target machine (Windows 10)_**

- Access Splunk via browser using the ip **_192.168.100.10:8000_**
- Download the _Universal Forwarder_ on Splunk website, make sure to select the correct OS, in our case it's Windows that runs in 64-bit
  - Double click the installer
  - Accept the License Agreement and select the **_An on-premise Splunk Enterprise instance_**
  - Type a _username_ and leave the _Generate random password_ checked
  - Skip the _Deployment Server_
  - _Receiving Indexer_ is the Splunk Server _192.168.100.10_ and port is _9997_ when receiving events

**_Sysmon_**

- Download _Sysmon_ installer on Windows 10
- Search in Google _Sysmon olaf config_ and download the _sysmonconfig.xml_
- Open Powershell in Administrator mode

  ![Configure Sysmon](./images/Sysmon.PNG)

- **Important:** Create a file _inputs.conf_ and save in **C:\Program Files\SplunkUniversalForwarder\etc\system\local** folder, this will instruct Splunk Forwarder on what we want to send over to Splunk Server

  ![Inputs Conf File](./images/InputsConf.PNG)

- Change the Log on as _Local System account_ and restart Splunk Universal Forwarder Service

  ![Splunk Forwarder](./images/SplunkForwarderService.PNG)

**_Splunk Web Portal Configuration_**

- Go to Splunk Web Portal and use the credentials you created during the installation

![Splunk Web Portal](./images/SplunkWeb1.PNG)

- Create an index. Go to _Settings_ -> _Index_ -> _New Index_ then Save

![Splunk Web Portal](./images/SplunkWeb2.PNG)

- Enable Splunk Server to receive the data. Go to _Settings_ -> _Forwarding and receiving_ -> Under the _Receive data_ section click _Add new_ and type _9997_ then click save

![Splunk Web Portal](./images/SplunkWeb3.PNG)

- Go to _Apps_ -> _Search & Reporting_ to test if data is coming in from Windows 10 machine (**Note:** I also configured my Domain Controller that's why you see 2 hosts in the image below, same configuration applies when you configure the DC machine)

![Splunk Web Portal](./images/SplunkIndex.PNG)

### Adding Windows 10 machine to Domain Controller

- Make sure your DNS points to our Domain Controller IP address or you will encounter an error. Open _Network and Internet settings_ -> _Change adapter options_ -> Right click adapter and select _Properties_

![Splunk Web Portal](./images/ADDS10.PNG)

- Search for _PC_ -> click _Properties_ -> click _Advanced system settings_ -> Enter the administrator account when prompted -> Go to _Computer Name_ tab -> Click _Change_ and enter the Domain you created -> _Restart_ the machine to apply changes

  ![Splunk Web Portal](./images/ADDS13.PNG)

- Test a user you created in you Domain Controller

  ![Splunk Web Portal](./images/ADDS9.PNG)
  ![Splunk Web Portal](./images/ADDS14.PNG)

### Test a Brute-force attack on Windows 10 machine

- Configure the Kali with a static IP based on our diagram. After the configuration try to Disconnect and Reconnect for the changes to take effect

  ![Splunk Web Portal](./images/Kali1.PNG)

- Create a directory _ADProject_ under Desktop
  - `mkdir ADProject`
- Copy _rockyou.txt.gz_ located in _/usr/share/wordlists/_ and unzip it using _gunzip_ then copy the unzip file to ADProject
  - `cd /usr/share/wordlists/`
  - `sudo gunzip rockyou.txt.gz`
  - `cp rockyou.txt ~/Desktop/ADProject`
  - `cd ~/Desktop/ADProject`
- Copy the first couple of lines of rockyou.txt to password.txt
  - `head -n 14 rockyou.txt > password.txt`
- Add the password of your user in _password.txt_ file
  - `nano password.txt` to edit it and add the password then save it
- Enable Remote Desktop on Windows 10 machine
  - Search for _PC_ -> click _Properties_ -> click _Advanced system settings_ -> Enter Administrator account when prompted

  ![Splunk Web Portal](./images/Kali3.PNG)

- Try the brute force attack using _Hydra_

  ![Splunk Web Portal](./images/Kali4.PNG)

- Check the Splunk telemetry. You can see 15 events with _Event Code = 4625_ indication of failed login in a span of milliseconds.

  ![Splunk Web Portal](./images/Kali5.PNG)
