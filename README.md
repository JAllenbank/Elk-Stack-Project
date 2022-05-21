## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![TODO: Update the path with the name of your diagram](https://github.com/JAllenbank/Elk-Stack-Project/blob/28440d7f383aa6dc6558beb7d72d0e9fb7f2cc9a/Diagrams/wk13elk.jpg)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the configuration files may be used to install only certain pieces of it, such as Filebeat.

[Filebeat-Config](https://github.com/JAllenbank/Elk-Stack-Project/blob/28440d7f383aa6dc6558beb7d72d0e9fb7f2cc9a/Ansible/Filebeatconfig.txt)

[Filebeat-Playbook](https://github.com/JAllenbank/Elk-Stack-Project/blob/28440d7f383aa6dc6558beb7d72d0e9fb7f2cc9a/Ansible/filebeat-playbook.txt)

This document contains the following details:

Description of the Topology
Access Policies
ELK Configuration
Beats in Use
Machines Being Monitored
How to Use the Ansible Build
  
  ### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly secure, in addition to restricting access to the network.
- Load balancers add resiliency by rerouting live traffic from one server to another if a server falls prey to a DDoS attack or otherwise becomes unavailable.
- A Jump Box Provisioner is also important as it prevents Azure VMs from being exposed via a public IP Address.  This allows us to do monitoring and logging on a single box.  We can also restrict the IP addresses able to communicate with the Jump Box, as we've done here.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the network and system logs.
- Filebeat collects data about the file system.
- Metricbeat collects machine metrics such as uptime.

The configuration details of each machine may be found below.

| Name      | Function           | IP Address | Operating System |
|-----------|--------------------|------------|------------------|
| Jump Box  | Gateway            | 10.0.0.1   | Linux            |
| Web VM1  | Azure VM           | 10.0.0.5   | Linux            |
| Web VM2  | Azure VM           | 10.0.0.6  | Linux            |
| ELK-Server| Analytics Platform | 10.1.0.4  | Linux            |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jump Box Provisioner machine can accept connections from the Internet. 

Machines within the network can only be accessed by my home IP address.

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------|
| Jump Box | Yes                 | 20.22.89.30        |
| Web VM1 | No                  | 10.0.0.5             |
| Web VM2 | No                  | 10.0.0.5             |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because it allows for setup in minutes using OpenSSH without installing anything on the servers.


The playbook implements the following tasks:
- Install Docker.io
- Install Python-pip
- Increase Virtual Memory
- Download and Launch ELK Docker Container (image sebp/elk)
- Published ports 5601 and 9200 were made available 

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![TODO: Update the path with the name of your screenshot of docker ps output](https://github.com/JAllenbank/Elk-Stack-Project/blob/2b06215a4e5b07925002217e1f2b0a9acd93be02/images/ELk%20VM%20PS.jpg)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- Web VM1 10.0.0.5
- Web VM2 10.0.0.6

We have installed the following Beats on these machines:
- Metricbeat 
- Filebeat 

These Beats allow us to collect the following information from each machine:
- Filebeat will be used to collect log files from very specific files such as Apache, Azure tools and web servers.
- Metericbeat will be used to monitor VM stats, per CPU core stats, per filesystem stats, memory stats and network stats.

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- SSH into the ELK Container ssh ansible@10.1.0.4 for my setup
- Run docker container list -a to verify that the container is on.
- Exit the ELK Container
- Navigate to (Your IP Address):5601 from your web browser.
- Open your ELK server homepage
- Click on Add Log Data.
- Click on the DEB tab under Getting Started to view the correct Linux Filebeat installation instructions.
- Choose System Logs.

- Copy the filebeat-playbook.yml file to /etc/ansible/roles

[Filebeat Playbook](https://github.com/JAllenbank/Elk-Stack-Project/blob/de59ad9d72e7d5e5c82ec05fd9435b1c84a5ced4/Ansible/filebeat-playbook.txt)

- Copy the filebeat-configuration.yml file to /etc/ansible/files.

[Filebeat Configuration](https://github.com/JAllenbank/Elk-Stack-Project/blob/28440d7f383aa6dc6558beb7d72d0e9fb7f2cc9a/Ansible/Filebeatconfig.txt)

- Scroll to line #1106 and replace the IP address with the IP address of your ELK machine, 10.1.0.4 for the purposes of my setup.
- Scroll to line #1806 and replace the IP address with the IP address of your ELK machine, 10.1.0.4 for the purposes of my setup.
- Run the playbook with ansible-playbook filebeat-configuration.yml.
- Next, confirm that the ELK stack was receiving logs. 
- Navigate back to the Filebeat installation page on the ELK server GUI.
- Verify that your playbook is completing Steps 1-4.
- On the same page, scroll to Step 5: Module Status and click Check Data.
- Scroll to the bottom and click on Verify Incoming Data.
- If the ELK stack was successfully receiving logs, you would have seen:

![TODO: Update the path with the name of your screenshot of ELK Filebeat](https://github.com/JAllenbank/Elk-Stack-Project/blob/9f9b818f552223709c2984021a4ae3d2b6800ddb/images/filebeatgettingdata.png)

- Repeat the steps for the Metricbeat

- Copy the metricbeat-configuration.yml file to /etc/ansible/files.

[Metricbeat Configuration](https://github.com/JAllenbank/Elk-Stack-Project/blob/28440d7f383aa6dc6558beb7d72d0e9fb7f2cc9a/Ansible/Metricbeatconfig.txt)

- Copy the metricbeat-configuration.yml file to /etc/ansible/files.

[Metricbeat Playbook](https://github.com/JAllenbank/Elk-Stack-Project/blob/2b06215a4e5b07925002217e1f2b0a9acd93be02/Ansible/Metricbeat-playbook.yml)

- Scroll to line #1106 and replace the IP address with the IP address of your ELK machine, 10.1.0.4 for the purposes of my setup.
- Scroll to line #1806 and replace the IP address with the IP address of your ELK machine, 10.1.0.4 for the purposes of my setup.

- Run ansible-playbook metricbeat-configuration.yml
- To verify that your play works as expected, on the Metricbeat installation page in the ELK server GUI, scroll to Step 5: Module Status and click Check Data.
