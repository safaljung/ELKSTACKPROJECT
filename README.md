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
| Web 3   | Webserver | 10.0.0.9   | Linux            |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jumpbox provisiner machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:

IP Address: 24.6.4.51

Machines within the network can only be accessed by ansible.

The Elk VM can be accessed through my Jumpbox Provisinor via ssh. The web 1 ,2 and 3 servers actively send data to ELK VM via ports 9200 and 5601. The IP Address is : 10.2.0.4.

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
- _TODO: List the IP addresses of the machines you are monitoring_

We have installed the following Beats on these machines:
- _TODO: Specify which Beats you successfully installed_

These Beats allow us to collect the following information from each machine:
- _TODO: In 1-2 sentences, explain what kind of data each beat collects, and provide 1 example of what you expect to see. E.g., `Winlogbeat` collects Windows logs, which we use to track user logon events, etc._

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the _____ file to _____.
- Update the _____ file to include...
- Run the playbook, and navigate to ____ to check that the installation worked as expected.

_TODO: Answer the following questions to fill in the blanks:_
- _Which file is the playbook? Where do you copy it?_
- _Which file do you update to make Ansible run the playbook on a specific machine? How do I specify which machine to install the ELK server on versus which to install Filebeat on?_
- _Which URL do you navigate to in order to check that the ELK server is running?

_As a **Bonus**, provide the specific commands the user will need to run to download the playbook, update the files, etc._
