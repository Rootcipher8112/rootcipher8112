# SOC-Automation-Project

## Objective

The SOC Automation Project aimed to build a simulated Security Operations Center (SOC) environment utilizing Security Orchestration, Automation, and Response (SOAR) capabilities. The primary objective was to demonstrate a real-world scenario of monitoring network hosts for malicious files. Using Shuffle, the Security Information and Event Management (SIEM) system was connected to VirusTotal to analyze suspicious files and determine their malicious nature. The output was then sent to TheHive to create an alert and subsequent case. Simultaneously, an email was dispatched to an analyst, providing relevant information for prompt remediation.

## Implementation Details

- **SIEM Setup:** Built a SIEM with Wazuh on a Digital Ocean cloud server running Ubuntu 22.04.
- **Log Collection:** Configured the SIEM to collect logs from a Windows 11 client, a Windows 10 client, and an Ubuntu client.
- **Integration with Shuffle.io:** Utilized Shuffle.io to connect the SIEM to VirusTotal using an API call for analyzing JSON data derived from the file, specifically its hash.
- **Alert Creation:** Leveraged the output from VirusTotal to create an alert on TheHive using an API call.
- **Notification to Analyst:** Automated the process of sending an email to the analyst containing all relevant data for quick and effective remediation.

## Skills Learned

- Advanced utilization of SOAR capabilities in a simulated SOC environment.
- Proficiency in setting up and configuring a Wazuh-based SIEM on a cloud server.
- Hands-on experience in collecting and analyzing logs from diverse client operating systems.
- Integration of external services (VirusTotal, TheHive) using API calls for enhanced threat analysis and response.
- Automated incident response and notification procedures for efficient security remediation.

## Automation Workflow

1. **Log Collection:** SIEM collects logs from different client operating systems.
2. **Shuffle.io Integration:** Shuffle.io connects the SIEM to VirusTotal for file analysis.
3. **VirusTotal Analysis:** VirusTotal pulls hash report based on sha256 hash.
4. **Alert Generation:** TheHive generates an alert based on the analysis output.
5. **Case Creation:** TheHive creates a case for tracking and managing the incident.
6. **Analyst Notification:** Automated email sent to the analyst with comprehensive data for remediation.

## SOAR Workflow 
![socprojectflow](https://github.com/Rootcipher8112/SOC-Automation-Project/assets/123340212/4b3496be-0804-4437-9cb8-6b7c33f2aa9b)

                                                           
## Steps

### Initial Setup
For this lab there were multiple setup steps before getting started with the bulk of the configurations to make this workflow run correctly. For the cloud machines I used Digital Ocean but any cloud provider can be used. For the local virtual machines I used Virtual box just for personal preference.

- **Machines to setup**:
  1. Wazuh Manager (ubuntu 22.04 cloud machine *8GB Ram minimum)
  2. TheHive Server (ubuntu 22.04 cloud machine *8GB Ram minimum)
  3. Wazuh Agents
     
     a. Windows 11 (local Machine : theSOC)
     
     b. Windows 10 (virtual machine on local host)
     
     c. Ubuntu 22.04 (virtual machine on local host)
     
- **Tool Setup**
  1. Shuffle.io
  2. VirusTotal (free account works fine but has limit of 500 API calls a day) 
  3. Email account (Used for Analyst notification. Used gmail for this lab)
##
**IMPORTANT SETUP INFORMATION FOR CLOUD FIREWALL**

<img width="573" alt="digidash" src="https://github.com/Rootcipher8112/SOC-Automation-Project/assets/123340212/0ee076ca-1080-4be1-9002-1b60ba0159ee">

##
**After creating our cloud machines we need to configure some firewall rules before we begin installing our tools.** 

<img width="507" alt="firewall" src="https://github.com/Rootcipher8112/SOC-Automation-Project/assets/123340212/beb6dbe1-eac9-4900-b8d1-ee3e6e04a94e">

**For the purposes of this lab I have set 3 inbound rules:**
- SSH on port 22 only from my local host public IP address (So only I can SSH into the machines)
- HTTPS on port 443 from my local host public IP address (so only I can access the Wazuh Dashboard)    
- TCP on port 9000 (This will be necessary for communication with TheHive later)
##

### Configuring Wazuh Manager

As I mentioned before the Wazuh manager is installed on an Ubuntu 22.04 cloud machine hosted on Digital Ocean. Setup is fairly straight forward the only configuration steps that are important is the amound of RAM and storage needed. The Wazuh documentation recommends a minimum of 8GB of RAM and 50GB of storage to operate correctly. 


Once setup we can deploy the machine. We are going to need to find the public IP address. We will be using ssh from our local machine to access this machine and continue with Wazuh setup.

![image](https://github.com/Rootcipher8112/SOC-Automation-Project/assets/123340212/f496de78-ef8f-44e1-9662-3877c5028710)

The next step is to download Wazuh Manager to the newly setup server.

**Download and configuration instructions can be found on the Wazuh website under DOCUMENTATION**

https://documentation.wazuh.com/current/quickstart.html 

To run the installation the following command can be entered: 

    curl -sO https://packages.wazuh.com/4.7/wazuh-install.sh && sudo bash ./wazuh-install.sh -a

When the installation finishes a message will be displayed with the login information. The default username is admin and a randomly generated password will be given. These will need to be written down.

![image](https://github.com/Rootcipher8112/SOC-Automation-Project/assets/123340212/1e8a6ae4-c06f-4bf1-9f04-0850723ef94c)


This information can accessed from the original zipped file if needed by entering the following command : 

    sudo tar -O -xvf wazuh-install-files.tar wazuh-install-files/wazuh-passwords.txt


On the local machine were going to head over to our favorite browser and navigate to https://**wazuh server IP address** and enter the credentials we saved in the previous step.

**Were presented with the following dashboard**
![image](https://github.com/Rootcipher8112/SOC-Automation-Project/assets/123340212/85f2e074-7422-4742-bac5-b7d5dc78075c)

### Adding Agents
The steps are basically the same to add agents to the different OSs were using for this lab.

![image](https://github.com/Rootcipher8112/SOC-Automation-Project/assets/123340212/9528e5b1-567a-452d-b6b0-401eda3da4db)

Were presented with this screen and need to pick a few options (we will do this twice in our lab   | **1 Widnows agent** | **1 Ubuntu agent** |
- Operating system
- Name for agent
- Wazuh manager to connect to
- optional configurations (this can be left blank for this lab)

Wazuh creates a script in the correct format for each OS. In this case for windows the script will be used on powershell and Ubuntu will be right in the bash terminal.
The script downloads, unzips and installs the wazuh agent service then configures the IP address which will be used to send logs. This again is our public IP address of the cloud machine.

Wazuh also provides the command to start up the service after installation. Once the service has been started on each machine we can head back over to the dashboard. 

If everything works correctly we should see a screen that looks like this:

![Screenshot 2024-01-23 115010](https://github.com/Rootcipher8112/SOC-Automation-Project/assets/123340212/bb85cdb4-d408-43c6-8396-97590fb88be7)
##
Now from here Wazuh will start ingesting logs from each machine based on default configurations. 

These configurations are held in the configuration file on the Wazuh Manager at:

      /var/ossec/etc/ossec.conf 


![image](https://github.com/Rootcipher8112/SOC-Automation-Project/assets/123340212/84e89155-622c-436f-9c49-558e176dfae7)

There are hundreds of settings that can be configured but for our lab these are the big ones be need setup
- Enable File Integrity Monitoring and set syscheck frequency to 60 (60 = 60 seconds, default is set to 12 hours which would not help us for this lab)
- Directories to check (for this lab I chose the downloads folder)
![image](https://github.com/Rootcipher8112/SOC-Automation-Project/assets/123340212/ed20236f-92b5-4afe-bf6d-a314462961b1)

**Another configuration we will be added later during shuffle configuration**

### IMPORTANT after configurations we will need to restart the wazuh manager using the following comman:

    systemctl restart wazuh-manager.service


## Navigating Wazuh

Now that we have agents communication with the Wazuh Manager there is a lot of interesting information we can see here:

## **Agent Dashboard**: here we can see our local machine theSOC
![Windows_agent_dashboard](https://github.com/Rootcipher8112/SOC-Automation-Project/assets/123340212/bb85c441-66e8-4f47-8f46-92d686982894)


## **File Integrity Monitoring**
![file_integrity_monitoring_windows_client](https://github.com/Rootcipher8112/SOC-Automation-Project/assets/123340212/3fc703f0-4c54-4a8f-8204-25d4045ca343)


## **MITRE ATT&CK Events**
![mitreatt ck_events_windows_client](https://github.com/Rootcipher8112/SOC-Automation-Project/assets/123340212/d9c2fc17-60c6-47ec-8e70-84af29256619)


## **Security Events**
![security_events_windows_client](https://github.com/Rootcipher8112/SOC-Automation-Project/assets/123340212/9bd1087e-0fe4-4aa6-af2d-5f723db6f945)


## **Vulnerabilties**
![vulnerabilities_windows_client](https://github.com/Rootcipher8112/SOC-Automation-Project/assets/123340212/75e0a48e-b052-4810-af66-37a3bb4c076d)


## **Security Configuration Assessment**
![sca_windows_client](https://github.com/Rootcipher8112/SOC-Automation-Project/assets/123340212/4254c72b-8625-4b6b-85dd-b72cbbf3d332)


##
Through this screen we can see a break down of CIS enterprise security benchmarks for specific Operating Systems, here he have Windows 11. We can then dig in and go through the passed and failed benchmarks. In a real world environment any failed benchmarks will need to be remediated to bring the operating system into compliance.

![failed_benchmark_windows_client](https://github.com/Rootcipher8112/SOC-Automation-Project/assets/123340212/7bbf8c25-a621-4133-885e-97fecdd1ac8f)


## At this point we can quickly recap what we've done:
- Setup cloud hosted machines for Wazuh and TheHive
- Setup Virtual Machines (Windows 10 and Ubuntu 22.04)
- Setup and configured Wazuh Manager on the cloud machine
- Setup Wazuh agents on the local host and both virtual machines
- Become familiar with the Wazuh Dashboard

### Next step is to download and configure TheHive on the other cloud machine

## Setting up TheHive

![image](https://github.com/Rootcipher8112/SOC-Automation-Project/assets/123340212/d514d372-4702-439e-9e9f-ae3e86fc1291)



**To begin this step we will need to ssh into our cloud machine using the public IP address found on the Digital Ocean dashboard.**

![image](https://github.com/Rootcipher8112/SOC-Automation-Project/assets/123340212/e8232bad-9658-44a6-bf27-9b9efcf098c1)


**Instructions to download and configure TheHive can be found on their site under DOCUMENTATION**
https://docs.strangebee.com/thehive/setup/

TheHive is a combination of three services (TheHive, Cassandra, and ElasticSearch)

These services can be downloaded and installed using the command line. There commands for many different linux distributions but for this case we are using Ubuntu 22.04 which is a Debian based linux so our command looks like this:
    
    wget -q -O /tmp/install.sh https://archives.strangebee.com/scripts/install.sh ; sudo -v ; bash /tmp/install.sh

This will download and setup the files we will need to install all three of these services.

Once completed we can start by installing and configuring Cassandra using this command:
    
    sudo apt update
    sudo apt install cassandra

Next we will need to configure the configuration file at this address:

    /etc/cassandra/cassandra.yaml

![image](https://github.com/Rootcipher8112/SOC-Automation-Project/assets/123340212/dbb540a9-d1bc-4a73-b9cd-340132d1b910)


We can see here that the cluster name I've chosen is 'mySOC'. This can be whatever you'd like but it will need to be configured.

Two other configurations we need to set are the "listen address" and "RPC address". These will be set to the 

![image](https://github.com/Rootcipher8112/SOC-Automation-Project/assets/123340212/80449241-93a8-4aed-8441-27d3f53fa6bc)
##
![image](https://github.com/Rootcipher8112/SOC-Automation-Project/assets/123340212/4b08c80d-e61b-486f-8269-1ce5d92253c7)

Then we can save the file and start Cassandra. To start the service we will use SystemD :

    sudo systemctl start cassandra

**Next we have to install and configure ElasticSearch. It is important setup and configure in this order as TheHive service will not start if the other 2 are not enabled first.**

To install ElasticSearch we first need to get the necessary repositories installed using the following commands:

    wget -qO - https://artifacts.elastic.co/GPG-KEY-elasticsearch |  sudo gpg --dearmor -o /usr/share/keyrings/elasticsearch-keyring.gpg
    sudo apt-get install apt-transport-https

    echo "deb [signed-by=/usr/share/keyrings/elasticsearch-keyring.gpg] https://artifacts.elastic.co/packages/7.x/apt stable main" |  sudo tee /etc/apt/sources.list.d/elastic-7.x.list 

Then we can install ElasticSearch:

    sudo apt update
    sudo apt install elasticsearch

With ElasticSearch installed we can move over to the configuration file to get a couple things set up:

    nano /etc/elasticsearch/elasticsearch.yml


![image](https://github.com/Rootcipher8112/SOC-Automation-Project/assets/123340212/e60d7802-6cb7-43f0-a0ac-ea80d3beb376)

In here we configure the "**cluster name**" and "**node name**". These can be whatever you'd like but to keep it simple I set them as shown above.

We also configure the network host which will be the public IP address of our 'thehive' cloud machine
![image](https://github.com/Rootcipher8112/SOC-Automation-Project/assets/123340212/5049c06f-e87b-4722-80bb-f5eca17b9285)

Now we can save and exit then start ElasticSearch with the following command:

    sudo systemctl start elasticsearch
    sudo systemctl enable elasticsearch

**IMPORTANT before we install TheHive we need to create the folder where logs will be stored on the cloud machine and give thehive permission to write to this folder.**

First create the folder using the following command:

    sudo mkdir -p /opt/thp/thehive/files

Then grant thehive permission using the following command:

    chown -R thehive:thehive /opt/thp/thehive/files

    

Finally we are ready to install TheHive and finish our setup. First to install we use this commands: 

    wget -O- https://archives.strangebee.com/keys/strangebee.gpg | sudo gpg --dearmor -o /usr/share/keyrings/strangebee-archive-keyring.gpg

    echo 'deb [signed-by=/usr/share/keyrings/strangebee-archive-keyring.gpg] https://deb.strangebee.com thehive-5.2 main' | sudo tee -a /etc/apt/sources.list.d/strangebee.list
    sudo apt-get update
    sudo apt-get install -y thehive

Next we need to configure a couple things configuration file at this address: 

    nano /etc/thehive/application.conf

![image](https://github.com/Rootcipher8112/SOC-Automation-Project/assets/123340212/86ff45fe-6c75-4edd-bea5-af48ce32e932)

The **"hostname"** will be the public IP address of thehive cloud machine as in previous steps. We also need to enter **cluster-name** (this is the cluster name configured with Cassandra), **keyspace**, and **index-name** which are both thehive (this is the cluster name from ElasticSearch which is deceiving). 

![image](https://github.com/Rootcipher8112/SOC-Automation-Project/assets/123340212/909f8267-73c1-4c41-97d9-edfafa77698f)

 
Lastly we need to configure the **Application service URL** which will be the address we enter to access the service in our web browser. By default the service is listening on port 9000 so all we need to do is add in our 'thehive' public IP address.

![image](https://github.com/Rootcipher8112/SOC-Automation-Project/assets/123340212/2c041b7f-9487-49d0-a19a-0526cae12a7e)

We can now save and exit as we have completed all necessary configurations. To start ElasticSearch we can use the following command:

    sudo systemctl start thehive
    sudo systemctl enable thehive

**IMPORTANT after enabling thehive check to make sure the service is actually running by checking the status with this command:**

    sudo systemctl status thehive


**If the status is DISABLED this most likely means one or both of our other services are not running.**

We can start both services again by running these commands:

    sudo systemctl start cassandra
    sudo systemctl start elasticsearch
    sudo systemctl enable thehive


We can then navigate to the following address in our web browser to access TheHive dashboard:

    https://**thehive IP address**:9000



**Default Credentials**

![image](https://github.com/Rootcipher8112/SOC-Automation-Project/assets/123340212/4de44709-c226-4d10-ad17-0f3281988099)



![image](https://github.com/Rootcipher8112/SOC-Automation-Project/assets/123340212/b1a99563-d6da-45ea-ba76-c06141326117)

Once in the dashboard we can change the admin password, add a default user for our analyst, and generate and API key to use later.

![image](https://github.com/Rootcipher8112/SOC-Automation-Project/assets/123340212/669e8159-ec11-4d9e-8ce3-4e20aebca92f)
##

![image](https://github.com/Rootcipher8112/SOC-Automation-Project/assets/123340212/cf6b1d20-47e6-44ec-bd59-5e88a79b49ca)
##

![image](https://github.com/Rootcipher8112/SOC-Automation-Project/assets/123340212/9ba35509-011e-4b47-8e90-8fad4321b392)


## Setting up Shuffle.io

![image](https://github.com/Rootcipher8112/SOC-Automation-Project/assets/123340212/75574167-016d-4b89-89e5-34d0c0bfa19c)


Shuffle is a tool used to create and manage workflows https://shuffler.io. For our lab we will utilize Shuffle to create a work flow which begins with a trigger from Wazuh that grabs json data for a specified use case. This data can then be filtered and enrished through the use of a VirusTotal API call. Then the results of that analysis are sent to TheHive to create an alert and finally automate an email, based on the information, to our Analyst for remdiation.

### Webhook Integration
First we will configure the Wazuh Manager with the shuffle integration in the configuration file. This integration will be attached to the **Webhook** feature within Shuffle. The webhook is a basic trigger function which can be configured in many different ways. For our use here I am going to configure the webhook to be triggered when a new file is downloaded into the **"Downloads"** folder on my wazuh agent.  In order to do this we are going to add the following to our /var/ossec/etc/ossec.conf file on our Wazuh Manager.

![image](https://github.com/Rootcipher8112/SOC-Automation-Project/assets/123340212/abd96a28-d70d-4d9c-8ab7-b7dd740d1092)

This integration can be configured in many different ways as mentioned. For example we could set the alert to trigger for severity level where there will be a trigger anytime a rule of that severity or higher is broken. For this lab we are looking at potentially malicious files being downloaded on a host.  In order to configure the integration for this we are using **rule_id 554** which is a rule in Wazuh related to a new file being added to a folder (in this case the Downloads folder) and the alert format should be set to json since this is the data format used by all of our tools.

The **hook_url** comes from Shuffle when the webhook app is added to the work flow:

![image](https://github.com/Rootcipher8112/SOC-Automation-Project/assets/123340212/e9dd350b-5b10-476a-9e10-09c4efe8153c)

### Gathering and Filtering JSON Data
We can then start the webhook and test it out by downloading a file on our host machine.

We should get back something like this on Shuffle:

![alert_exec](https://github.com/Rootcipher8112/SOC-Automation-Project/assets/123340212/0c72c32b-aeb5-4225-862b-a486ca043be7)

### VirusTotal Integration
Next we can add a VirusTotal app to our workflow.  VirusTotal is site that can analyse files, hashes, and urls for signatures of malware. This is a well known tool in cybersecurity and can be extremely useful.

![virustotal_homepage](https://github.com/Rootcipher8112/SOC-Automation-Project/assets/123340212/5d725e63-52f9-46e6-8322-903ba490fad4)

There is a paid version but the free version will work just fine for this lab. With the free version you are able to make 500 API calls a day again for us this is enough.  In the settings we can grab the API key and copy it over to Shuffle.

Now going through the json data we grabbed from the webhook we want to set our variable which VirusTotal uses to perform whatever function we want it to do. For our use case we want VirusTotal to give us a hash report. From the json data we see here **sha
256_after** this will be the variable we set in the VirusTotal app to give us our hash report.

![hash_value](https://github.com/Rootcipher8112/SOC-Automation-Project/assets/123340212/f6632916-b7e7-4a62-bb68-4a05898951d9)

We can run our workflow again with VirusTotal configured and should return something that looks like this:

![virustotal_output](https://github.com/Rootcipher8112/SOC-Automation-Project/assets/123340212/55f4da08-2d81-4c26-afc7-a24bd4dde56b)

### Connecting TheHive
We can then go through this report and find the information we would like to send over to TheHive and then configure a TheHive app within our workflow.

**Here we are going to use the API key we set up earlier as well as input all the variables associated with the information we will use to create an alert for our Analyst. This can be configured in many different ways based on use but for this lab We will add:**

- Timestamp
- host (Wazuh agent name)
- path of file
- VirusTotal Analysis (malicious or not)
- Malicious Score (VirusTotal analyzes the hash against up to 70 sources)
- Malware type
- File Hash
- MITRE rule

### Email Automation
Once we have confirmed this alert generates correctly we can add the final piece of our SOAR automation, the email to our Analyst. Again we will configure the app within shuffle with all of the data that went into our TheHive app but we will also configure suggestions based on the findings of the file.  In our case since we are dealing with a malicious file the out put will be **"Malicious File Detected!! Immediate remediation is required!!**

![socemail_inbox](https://github.com/Rootcipher8112/SOC-Automation-Project/assets/123340212/0ef2b695-548f-4155-91b9-556fe6ca7b16)



<img width="377" alt="new email pic" src="https://github.com/Rootcipher8112/SOC-Automation-Project/assets/123340212/d70f2a06-3560-42c4-ba32-6ee4ab2e9ca4">

## 
### Here is our finalized workflow on Shuffle:

![soar_setup](https://github.com/Rootcipher8112/SOC-Automation-Project/assets/123340212/5e1afd86-38e7-4d8a-8a8a-2e61639b4a71)


## Now that we have our SOAR automation set up we can run through and see how powerful this can be in a real world scenario.


# <a href="https://youtu.be/D61Ty8PN5fw">CLICK HERE FOR DEMONSTRATION</a>   

##
