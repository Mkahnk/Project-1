# Project-1
First project documenting the implementation of an ELK-stack on our azure cloud system.

## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

- /Diagrams/Azure_diagram.png

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the install-elk.yml file may be used to install only certain pieces of it, such as Filebeat.

- install-elk.yml
- filebeat.yml
- filebeat-playbook.yml
- metricbeat.yml
- metricbeat-playbook.yml

This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly available, in addition to restricting access to the network.
- Load balancers divide the load of a server and help ensure that if one node goes down the other nodes can take over the work and run smoothly until the node is back up and running.
- A Jump Box adds an extra layer of security since the machine(s) behind the jump box are on their own private network and must be accessed through the jump box.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the log files and system metrics.
- Filebeat collects and ships log files.
- Metricbeat records and collects various system level metrics.

The configuration details of each machine may be found below.
_Note: Use the [Markdown Table Generator](http://www.tablesgenerator.com/markdown_tables) to add/remove values from the table_.

| Name       |  Function                     | IP Address       | Operating System |
|------------|-------------------------------|------------------|------------------|
| ELK-Jump   | Gateway/ELK   		             | 10.0.0.9         | Linux            |
| DVWA VM1   | Backend Pool/Docker Container | 10.0.0.6         | Linux            |
| DVWA VM2   | Backend Pool/Docker Container | 10.0.0.8         | Linux            |
| RedTeam-LB | Load balancer		             | 13.91.288.105    | N/A              |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the ELK-Jump machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- 71.82.116.30, 10.0.0.6, 10.0.0.8

Machines within the network can only be accessed by ELK-Jump.
- the jump box is able to access the ELK server and has a private ip address of 10.0.0.9

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses           |
|----------|---------------------|--------------------------------|
| ELK-Jump | Yes                 | 10.0.0.6 10.0.0.8 71.82.116.30 |
| DVWA VM1 | No                  | 10.0.0.8 10.0.0.9              |
| DVWA VM2 | No                  | 10.0.0.6 10.0.0.9              |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
- The main advantage of automating configuration with Ansible is that every instance is easily repeatable and allows for easy scaling.  
- It also allows for everything to be done faster than if it were done manually.

The playbook implements the following tasks:
- Install docker.io: installs the debian version of docker
- Install python-pip: installs python-pip, a package management system used to install and manage packages written in python.
- Install Docker Module: installs the ansible module
- Increase virtual memory: This increases the memory and allows ELK to run uninterupted.
- Download and launch a Docker ELK container: This install the ELK container and starts it.

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

- /Images/docker_ps_output.png

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- 10.0.0.6
- 10.0.0.8

We have installed the following Beats on these machines:
- Filebeat
- Metricbeat

These Beats allow us to collect the following information from each machine:
- Filebeat: The most commonly used beat and collects log files and will show you logs such as: audit logs, server logs, and deprecation logs.
- Metricbeat: Collects various system level metrics such as cache size.

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the filebeat.yml file to /etc/ansible/files.
- Update the hosts file to include the private ip address of your machine(s)
- Run the playbook, and navigate to DVWA VM1 or DVWA VM2 to check that the installation worked as expected.

- filebeat-playbook.yml, copy it into /etc/ansible/roles
- Which file do you update to make Ansible run the playbook on a specific machine?: filebeat.yml. 
- How do I specify which machine to install the ELK server on versus which to install Filebeat on? hosts file for elk and filebeat.yml for filebeat
- Navigate to http://[your.VM.IP]:5601 to ensure that the ELK stack is running.

As a **Bonus**, provide the specific commands the user will need to run to download the playbook, update the files, etc.

