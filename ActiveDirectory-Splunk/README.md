# Active Directory Home Lab with Splunk & Attack Simulation

## Summary

This project demonstrates the setup of a fully functional cybersecurity home lab designed to simulate real-world attack scenarios and analyze generated telemetry.

The lab environment includes an Active Directory domain built on Windows Server 2022, a Windows 10 endpoint, and a Splunk SIEM instance deployed on an Ubuntu Server for centralized log collection. Logs are ingested from both the Domain Controller and the target machine (Windows 10) to provide visibility into system and security events.

To simulate adversarial activity, Kali Linux is used to perform a brute-force attack against the environment using Hydra.

This project also provides setting up of some of the environment in VirtualBox, including the installation and configuration of systems and tools.


Key Objectives:
* Build and configure an Active Directory lab environment
* Centralize log collection using Splunk
* Simulate brute-force attacks and adversary techniques
* Gain hands-on experience with red team concepts

**Not Included in this document but *required*:**

* Setting up of NAT Networks are not shown in this document, you may research on how to implement that.
* Configuring the Virtual Machines to use the NAT Network you created so they are on the same network and have intenet connectivity
* Creating of Shared Folders from Ubuntu to map the Splunk installer
* Adding of users to group ***vboxsf***


### Diagram

![Active Directory Home Lab Diagram](./images/Diagram.PNG)

### Tools


|Application| Description| Download link|
|----|----|----|
|Windows 10| Target machine|[Click here](https://www.microsoft.com/en-ca/software-download/windows10)|
| Windows Server 2022 |  Domain Controller |[Click here](https://www.microsoft.com/en-us/evalcenter/download-windows-server-2022)
|Ubuntu | Splunk Server|[Click here](https://ubuntu.com/download/server)
|Splunk|SIEM of choice|[Click here](https://www.splunk.com/en_us/download/splunk-enterprise.html?locale=en_us)
|Kali Linux| Attacker's machine|[Click here](https://www.kali.org/get-kali/#kali-virtual-machines)
|7-zip|To extract the Kali Linux VM|[Click here](https://www.7-zip.org/)
|Sysmon| To monitor and log system activity|[Click here](https://learn.microsoft.com/en-us/sysinternals/downloads/sysmon)|

### Installation

***Windows 10:***

* While downloading, select the following options in the pop-up window:
    * Create installation media
    * ISO file
* While installing, select the following options in the pop-up window:
    * I don't have a product key
    * Windows 10 Pro
    * Custom: Install Windows only (advanced)

![Windows 10 Installation](./images/Win10.PNG)

***Kali Linux:***

* I suggest to just download the pre-built virtual machine, check if you have a 32-bit or 64-bit machine so you know what to download
* You also need to download and install 7-zip to extract the Kali Linux VM
* After you extract the downloaded Kali VM, double click the ***.vbox*** file extension and it will automatically be imported to VirtualBox
* Default credentials for Kali Linux is ***kali/kali***


***Windows Server 2022:***

* Click on the **New** icon in VirtualBox, enter a Name, and select the **ISO** file you downloaded
* Select **Skip Unattended Installation**
* Select **Windows Server 2022 Standard Evaluation (Desktop Experience)**
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

* OUs (Organizational Units) and Users have been created but are not shown in the screenshots. Please ensure you create them as well, as they will be used when joining the Windows 10 machine to the domain.

***Ubuntu Server***

 * Similar to how you install the Windows Server 2022, click on the **New** icon in VirtualBox, enter a Name, and select the **ISO** file you downloaded
 * While installing, select the following options in the screen:
    * Try or Install Ubuntu Server
    * Continue without updating
    * In **Mirror check still running** screen, select **Continue**

    ![Credentials Info](./images/UbuntuSvr2.PNG)
    * Select **Continue** or **Done** until the setup starts installing
    * Select **Reboot Now** when it appears
    * Run the Update and Upgrade command
        * `sudo apt-get update && sudo apt-get upgrade -y`

* Create a static IP address (I'm using version 24, if you are using version 22 you might have different file e.g. ***00-installer-config.yaml***) 
* Add a DNS and Default Route
* Verify that the IP address has changed

![StaticIP](./images/Splunk_StaticIP.PNG)

![StaticIP](./images/Splunk_StaticIP_2.PNG)

![StaticIP](./images/Splunk_StaticIP_3.PNG)



***Splunk***

* Download Splunk Enterprise, select the Linux (.deb file)
* Install the highlighted packages add-ons for VirtualBox

![VirtualBoxAddons](./images/Splunk4.PNG)

* Install Splunk

![VirtualBoxAddons](./images/Splunk5.PNG)

* Change into the directory where Splunk is located into the server 

![VirtualBoxAddons](./images/Splunk6.PNG)

* Change into the user ***splunk*** using the below command
    * `sudo -u splunk bash`
* Change into ***bin*** directory and start the installation of Splunk
    * `cd bin`
    * `./splunk start`

* Run the commands below to ensure Splunk starts whenever the server reboots
    * `exit`
    * `cd bin`
    * `sudo ./splunk enable boot-start -user splunk`

![VirtualBoxAddons](./images/Splunk7.PNG)


***Installing Splunk Universal Forwarder in Target machine (Windows 10)***


* Access Splunk via browser using the ip ***192.168.100.10:8000***
* Download the Universal Forwarder on Splunk website, make sure to select the correct OS, in our case it's Windows that runs in 64-bit
    * Double click the installer
    * Accept the License Agreement and select the ***An on-premise Splunk Enterprise instance***
    * Type a *username* and leave the *Generate random password* checked
    * Skip the *Deployment Server*
    * *Receiving Indexer* is the Splunk Server *192.168.100.10* and port is *9997* when receiving events

***Sysmon***

* Download *Sysmon* installer on Windows 10
* Search in Google *Sysmon olaf config* and download the *sysmonconfig.xml*
* Open Powershell in Administrator mode

    ![Configure Sysmon](./images/Sysmon.PNG)

* **Important:** Create a file *inputs.conf* and save in **C:\Program Files\SplunkUniversalForwarder\etc\system\local**, this will instruct Splunk Forwarder on what we want to send over to Splunk Server

    ![Inputs Conf File](./images/InputsConf.PNG)

* Change the Log on as *Local System account* and restart Splunk Universal Forwarder Service

    ![Splunk Forwarder](./images/SplunkForwarderService.PNG)

***Splunk Web Portal Configuration***

* Go to Splunk Web Portal and use the credentials you created during the installation

![Splunk Web Portal](./images/SplunkWeb1.PNG)

* Create an index. Go to Settings -> Indexex -> New Index then Save

![Splunk Web Portal](./images/SplunkWeb2.PNG)

* Enable Splunk Server to recive the data. Go to Settings -> Forwarding and receiving -> Under the *Receive data* section click *Add new* and type *9997* then click save

![Splunk Web Portal](./images/SplunkWeb3.PNG)

* Go to Apps -> Search & Reporting to test if data in coming in from Windows 10 machine (**Note** I also configured my Domain Controller that's why you see 2 hosts in the image below, same configuration applies when you configure the DC machine)

![Splunk Web Portal](./images/SplunkIndex.PNG)


### Adding Windows 10 machine to Domain Controller

* Make sure you DNS points to our Domain Controller IP address or you will encounter an error. Open *Network and Internet settings* -> *Change adapter options* -> Right click adapter and select *Properties*

![Splunk Web Portal](./images/ADDS10.PNG)

* Search for *PC* -> click *Properties* -> click *Advanced system settings* -> Enter the administrator account when prompted -> Go to *Computer Name* tab -> Click *Change* and enter the Domain you created -> *Restart* the machine to apply changes

    ![Splunk Web Portal](./images/ADDS13.PNG)

* Test a user you created in you Domain Controller

    ![Splunk Web Portal](./images/ADDS9.PNG)
    ![Splunk Web Portal](./images/ADDS14.PNG)

### Test a Brute-force attack on Windows 10 machine

* Configure the Kali with a static IP based on our diagram. After the configuration try to Diconnect and Reconnect for the changes to take effect

    ![Splunk Web Portal](./images/Kali1.PNG)

* Create a directory *ADProject* under Desktop
    * `mkdir ADProject`
* Copy rockyou.txt.gz located in /usr/share/wordlists/ and unzip it using *gunzip* then copy the unzip file to ADProject
    * `cd /usr/share/wordlists/`
    * `sudo gunzip rockyou.txt.gz`
    * `cp rockyou.txt ~/Desktop/ADProject`
    * `cd ~/Desktop/ADProject`
* Copy the first couple of lines of rockyou.txt to password.txt
    * `head -n 14 rockyou.txt > password.txt`
* Add the password of your user in *password.txt* file
    * `nano password.txt` to edit it and add the password then save it
* Enable Remote Desktop on Windows 10 machine
    * Search for *PC* -> click *Properties* -> click *Advanced system settings* -> Enter Administrator account when prompted
    ![Splunk Web Portal](./images/Kali3.PNG)

* Try the brute force attack using *Hydra*
    ![Splunk Web Portal](./images/Kali4.PNG)

* Check the Splunk telemetry. You can see 15 events with *Event Code = 4625* indication of failed login in a span of milliseconds.
    ![Splunk Web Portal](./images/Kali5.PNG)
