## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

https://github.com/safaljung/kcproject13/blob/8189640c059c75a3486913dcdad61b24f5fa31c9/Diagrams/X_corp.jpg

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the Filebeat-playbook.yml file may be used to install only certain pieces of it, such as Filebeat.

Elk-playbook.yml
Filebeat-config.yml
Filebeat-playbook.yml
Metricbeat-config.yml
Metricbeat-playbook.yml
Webservers-playbook.yml



This document contains the following details:
- Description of the Topology 
- Access Policies
- ELK Configuration
- Beats in Use
- Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly protected and secure, in addition to restricting access to the network.

Load Balancers do the process of distributing network traffic accross multiple servers and spread the work evenly accross the servers which improves application responsiveness. A load balancer can act as a reverse proxy and distributes network or application traffic across a number of server. The Load Balancer protects the organization against distributed denial-of-service (DDoS) attacks by malicous actors. 

Jumpobox is a system on a the network which only has access for management of our webservers within a system enviroment which can be accessed on port 80. It acts an a layer of security which prevents our Azure servers from being exposed to the public.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the Logs and system Metrics.

Filebeat consists of two main components: inputs and harvesters. These components work together to monitor the log files and send event logs to the output to Kibana.

Metricbeat records metrics from our system and services. It includes system-level CPU to memory usage, Redis to NGINX, file system, disk IO, and network IO statistics, as well as top-like statistics for every process running on the system.

The configuration details of each machine may be found below.

| Name    | Function  | IP Address | Operating System |
|---------|-----------|------------|------------------|
| Jumpbox | Gateway   | 10.0.0.5   | Linux            |
| Web 1   | Webserver | 10.0.0.7   | Linux            |
| Web 2   | Webserver | 10.0.0.9   | Linux            |
| Web 3   | Webserver | 10.0.0.10  | Linux            |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jumpbox Provisioner machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:

IP Address: 24.6.4.51

Machines within the network can only be accessed by ansible.

The Elk VM can be accessed through my Jumpbox Provisioner via ssh. The web 1 ,2 and 3 servers actively send data to ELK VM via ports 9200 and 5601. The IP Address is : 10.2.0.4.

A summary of the access policies in place can be found in the table below.

| Name    | Publicly Accessible | Allowed IP Address |
|---------|---------------------|--------------------|
| Jumpbox | Yes                 | 24.6.4.51          |
| Web 1-3 | Yes                 | 13.92.170.196      |


Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because patch fixes, updates can be performed very efficiently by selecting entire machines on the network.


The playbook implements the following tasks:

Installation of Docker
Installation of Pip3 (python)
Installation of Python Docker Module
Installation of Metricbeat
Installation of Filebeat
Enables Docker on Boot
Download and launch Docker Elk container on Elk Server VM

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![TODO: Update the path with the name of your screenshot of docker ps output](Images/docker_ps_output.png)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
Web 1 10.0.0.7
Web 2 10.0.0.9
Web 3 10.0.0.10

We have installed the following Beats on these machines:
 Filebeats on Web Server 1, 2 and 3. Metricbeat on Web Server 1,2 and 3.

These Beats allow us to collect the following information from each machine:

Filebeat is a logging agent installed on the  Web Servers, tailing them, and forwarding the data to Kibana VM for more advanced processing or directly into Elasticsearch for indexing. It is essentially a log forwarding tool that itemized and tracks all files on the server and reports changes to them.

Metricbeat is a lightweight shipper that we can install on our servers to periodically collect metrics from the operating system and from services running on the server. Metricbeat helps you monitor your servers by collecting metrics from the system and services running on the server, such as:

Apache

HAProxy

MongoDB

MySQL

Nginx





### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the Config file to etc/ansible/config.
- Update the Config file to include the Elk Server internal ip adderess. 
- Run the playbook, and navigate to kibana to check that the installation worked as expected.


- Which file is the playbook? Where do you copy it?

The playbook is Filebeat-playbook.yml, Metricbeat-playbook.yml, Elk-playbook.yml and Webservers-playbook.yml
 
 We need to copy them in etc/ansible/playbooks in the ansible in Jummpbox.
 
Which file do you update to make Ansible run the playbook on a specific machine? How do I specify which machine to install the ELK server on versus which to install Filebeat on?

We need to update the hosts file to make ansible run the playbook on specific machines. We specify selecting the group Webservers and Elk in the hosts file to install ELK server on versus which to install Filebeat.


Which URL do you navigate to in order to check that the ELK server is running?

We need to go to this url:

http://13.88.158.162:5601/app/kibana#/home

!3.88.158.162 is the Public ip address of the server where as 5601 is the port.


As a **Bonus**, provide the specific commands the user will need to run to download the playbook, update the files, etc.




They can download the playbook by 
curl  https://github.com/safaljung/kcproject13/tree/main/Ansible. and copy it to thier etc/ansible directory with speicific direcotry for config and playbooks. 

They need to update the congig file with the ip address of our elk server so the Filebeat and MetricBeat on web 1 ,2 and 3 sends the data to the Elk Server.

nano hosts in the ansible directory and on the Webservers Group we need to put the ip address of our Web 1, 2 and 3, where as in the group ELk we put the ip address of your Elk Machine.

after editing the nano files and config files, the user can run 

sudo ansible-playbook Elk-playbook.yml To Install Elk docker on Elk server


sudo ansible-playbook Filebeat-playbook.yml To Install Filebeat on Webservers  

sudo ansible-playbook Metricbeat-playbook.yml To install Metricbeat on Webserves

sudo ansible-playbook Webservers-playbook.yml To install Docker, Python,  Python Docker Module and Docker Web Contianer.

