# ELK Project 1
## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![Diagram Project 1](https://user-images.githubusercontent.com/81339363/130390367-0ec2d41d-f9b2-4aff-81c4-1b14f9bc6925.jpg)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the YAML file may be used to install only certain pieces of it, such as Filebeat.

YAML File to Install Filebeat

https://github.com/alims86/ELK-Project/blob/main/Ansible/Filebeats/Filebeats%20Playbook%20YML.jpg


This document contains the following details:
- Description of the Topologu
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly available, in addition to restricting access to the network.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the filesystem and system performance.

Filebeat watch the logs,collect log evernt.
Metricbeat watch the system performance (CPU,MEMORY,Network Traffic).


![Table 1](https://user-images.githubusercontent.com/81339363/130533364-0501aa88-8c1f-430e-bbd4-6084421c9aa4.jpg)


### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jump Box machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
 (My Home Public IP)

Machines within the network can only be accessed by Jump Box or ELK Machine.
Jump box ( 10.0.0.10) & ELK Machine  ( 10.2.0.5)

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------|
| Jump Box | Yes                 | My Home Public IP    |
| Web3     | No                  | Local Vnet           |
| Web4     | No                  | Local Vnet           |
| ELK2     | Yes                 | My Home Public IP    |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
It reduce the errors and increase prodoctivity.

The playbook implements the following tasks:
1. Configue the Webservers.
2. Install ELK
3. Install Filebeat
4. Install Metricbeat

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![ELK Docker PS](https://user-images.githubusercontent.com/81339363/130390559-265af6d2-a267-4693-ad18-e3ed53d8324c.jpg)


### Target Machines & Beats
This ELK server is configured to monitor the following machines:

| Name     | Function                                | IP Address | Operating System |
|----------|---------------------- ------------------|------------|------------------|
| Web3     | Host a container(DVWA)                  |  10.0.0.13 | Linux            |
| Web4     | Host a container(DVWA)                  |  10.0.0.14 | Linux            |


We have installed the following Beats on these machines:
1.Filebeat
2.Metricbeat

These Beats allow us to collect the following information from each machine:
1. Filebeat collects linux logs. This allows us to track things like user logon events, failed access attempts, service starts and stops.
2. Metricbeat collects system metrics from the web servers. We look for things like cpu usage, memory usage, drive space usage and drive space available for each host.

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the /etc/ansible/roles to etc/ansible/files.
- Update the host file to include the IP addresses of the VMs.
- Run the playbook, and navigate to http://elkserverPublicIP/setup.php to check that the installation worked as expected.

_TODO: Answer the following questions to fill in the blanks:_
- _Which file is the playbook? Where do you copy it? Host file and Copy Hosts to etc/Anisble
- _Which file do you update to make Ansible run the playbook on a specific machine? How do I specify which machine to install the ELK server on versus which to install Filebeat on? The hosts file to include the Webservers Private IPs and ELK IP.
- _Which URL do you navigate to in order to check that the ELK server is running?  http://20.57.177.19:5601/app/infra#/infrastructure/inventory





