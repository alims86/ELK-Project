# ELK Project 1
## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

Diagram_Project_1.jpg

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the YAML file may be used to install only certain pieces of it, such as Filebeat.

YAML File to Install Filebeat

---
  - name: installing and launching filebeat
    hosts: webservers
    become: yes
    tasks:

    - name: download filebeat deb
      command: curl -L -O https://artifacts.elastic.co/downloads/beats/filebeat/filebeat-7.6.1-amd64.deb

    - name: install filebeat deb
      command: dpkg -i filebeat-7.6.1-amd64.deb

    - name: drop in filebeat.yml
      copy:
        src: /etc/ansible/files/filebeat-config.yml
        dest: /etc/filebeat/filebeat.yml

    - name: enable and configure system module
      command: filebeat modules enable system

    - name: setup filebeat
      command: filebeat setup

    - name: start filebeat service
      command: service filebeat start

    - name: enable service filebeat on boot
      systemd:
        name: filebeat
        enabled: yes


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
- _TODO: What aspect of security do load balancers protect? What is the advantage of a jump box?_

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the filesystem and system performance. The ELK stack is in a separate region and virtual network. This helps separate operational services with production services.

The configuration details of each machine may be found below.
_Note: Use the [Markdown Table Generator](http://www.tablesgenerator.com/markdown_tables) to add/remove values from the table_.

| Name     | Function                                | IP Address | Operating System |
|----------|---------------------- ------------------|------------|------------------|
| Jump Box | Gateway                                 |  10.0.0.10 | Linux            |
| Web3     | Host a container(DVWA)                  |  10.0.0.13 | Linux            |
| Web4     | Host a container(DVWA)                  |  10.0.0.14 | Linux            |
| ELK2     | Monitoring & log aggregation for Web3&4 |  10.2.0.5  | Linux            |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jump Box machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
98.196.162.255 (My Local Home IP)

Machines within the network can only be accessed by Jump Box or ELK Machine.
Jump box ( 10.0.0.10)  ELK Machine  ( 10.2.0.5)

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------|
| Jump Box | Yes                 | 98.196.162.255       |
| Web3     | No                  | Local Vnet           |
| Web4     | No                  | Local Vnet           |
| ELK2     | Yes                 | 98.196.162.255       |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
- _TODO: What is the main advantage of automating configuration with Ansible?_

The playbook implements the following tasks:
- _TODO: In 3-5 bullets, explain the steps of the ELK installation play. E.g., install Docker; download image; etc._
- ...
- ...

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![TODO: Update the path with the name of your screenshot of docker ps output](Images/docker_ps_output.png)

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
- Copy the Ansible.cfg file to etc/ansible.
- Update the host file to include the IP addresses of the VMs.
- Run the playbook, and navigate to Ansible/yml file to check that the installation worked as expected.

_TODO: Answer the following questions to fill in the blanks:_
- _Which file is the playbook? Where do you copy it?_
- _Which file do you update to make Ansible run the playbook on a specific machine? How do I specify which machine to install the ELK server on versus which to install Filebeat on?_
- _Which URL do you navigate to in order to check that the ELK server is running?

_As a **Bonus**, provide the specific commands the user will need to run to download the playbook, update the files, etc._



