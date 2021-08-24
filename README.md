# ELK Project 1
## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![Diagram Project 1](https://user-images.githubusercontent.com/81339363/130390367-0ec2d41d-f9b2-4aff-81c4-1b14f9bc6925.jpg)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the YAML file may be used to install only certain pieces of it, such as Filebeat.

YAML File to Install Filebeat

https://github.com/alims86/ELK-Project/blob/main/Ansible/Filebeats/Filebeats%20Playbook%20YML.jpg


This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build

### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the DVWA Vulnerable Web Application.

Load balancing ensures that the application will be highly available, in addition to restricting access to the network.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the filesystem and system performance.

Filebeat watch the logs,collect log evernt.
Metricbeat watch the system performance (CPU,MEMORY,Network Traffic,etc...).


![Table 1](https://user-images.githubusercontent.com/81339363/130533364-0501aa88-8c1f-430e-bbd4-6084421c9aa4.jpg)


### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jump Box machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
 (My Home Public IP)

Machines within the network can only be accessed by Jump Box or ELK Machine.
Jump box (10.0.0.10) & ELK Machine (10.2.0.5)

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

![Table 2](https://user-images.githubusercontent.com/81339363/130541296-cac97feb-cbb7-41cb-ac87-b86016a84a74.jpg)


We have installed the following Beats on these machines:
1.Filebeat
2.Metricbeat

These Beats allow us to collect the following information from each machine:
1. Filebeat collects linux logs. This allows us to track things like user login events, failed access attempts, service starts and stops.
2. Metricbeat collects system metrics from the web servers. We look for things like cpu usage, memory usage, drive space usage and drive space available for each host.

### Using the Playbook 

Copy the ansible.cfg file to /etc/ansible.
Update the hosts file to include the DVWA Vitrual Machines Private IP Addresses and ELK Private IP Address.
Run the playbook etc/ansible/roles/metric-playbook.yml and navigate to the ELK server on port tcp 5601 to ensure to check that the installation worked as expected with the following URL: http://20.57.177.19:5601/app/kibana#/home


