## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

/Images/Elk_Server_Diagram


This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly reliable while enabling more network traffic, in addition to restricting unauthorized users to the network.
- While the load balancer allows keeps availability at its peak, the jumpbox allows for any Red Team member access for further penetration testing

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the _____ and system _____.
- Filebeat is a shipper for logs and data regarding network traffic.
- Metricbeat monitors system metrics such as CPU and memory usage and any anomalies that may occur.

The configuration details of each machine may be found below.
_Note: Use the [Markdown Table Generator](http://www.tablesgenerator.com/markdown_tables) to add/remove values from the table_.

| Name       | Function   | IP Address              | Operating System |
|------------|------------|-------------------------|------------------|
| Jump Box   | Gateway    | 10.0.0.4                | Linux            |
| VM 1       | Shipper    | 10.0.0.5                | Linux            |
| VM 2       | Shipper    | 10.0.0.7                | Linux            |
| Elk Server | Holds Logs | 10.0.0.9, 51.143.89.116 | Linux            |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the jump box machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
-To the jump box, the only whitelisted IP was linked to the SSH key


Machines within the network can only be accessed by the Jump Box.
- The Elk container can be accessed by the jump box (IP: 10.0.0.4

A summary of the access policies in place can be found in the table below.

| Name          | Publicly Accessible | Allowed IP Addresses |
|---------------|---------------------|----------------------|
| Jump Box      | Yes (by ssh key)    | 10.0.0.5 10.0.0.7    |
| Load Balancer | Yes                 | 10.0.0.5 10.0.0.7    |


### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
- Having the playbook to automate the deployment of more machines in the network. This will save time and resources down the line as well as having all machines configured precisely to the playbook without any discrepancies.


The playbook implements the following tasks:
- Install Docker
- Install PIP
- Install python module
- Increase virtual memory
- Install and start the ELK docker container.

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

/Images/Day 1.png

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- 10.0.0.4
- 10.0.0.5
- 10.0.0.7

We have installed the following Beats on these machines:
- Filebeat
- Metricbeat

These Beats allow us to collect the following information from each machine:
- Filebeat monitors event logs and then ships to the Elk server. Metricbeat covers all the system metrics such as CPU, memory, and network IO statistics.
### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the filebeatconfig.yml and metricbeatconfig.yml files to the '/etc/ansible/files' directory
- Update the filebeatconfig.yml and metricbeatconfig.yml files to include the ELK ip as outputs.
- Run the filebeat-playbook.yml (ansible-playbook filebeat-playbook.yml)
- Navigate to Kibana (10.0.0.9:5601) and make ensure the incoming data.

_TODO: Answer the following questions to fill in the blanks:_
- _Which file is the playbook? Where do you copy it?: The playbook is 'filebeat-playbook.yml' and it should be located in the '/etc/ansible/files' directory.
- _Which file do you update to make Ansible run the playbook on a specific machine? How do I specify which machine to install the ELK server on versus which to install Filebeat on?:
First the hosts configuration file should have be configured to have VM1 and VM2 under [webservers] and the ELK server IP should be under [elkserver]. The playbooks will have a determined value
to install on either [webservers] or [elkserver] according to the playbook
- To ensure all is working, navigate to the elkserver's public ip and port 5601 since that is the established port [52.143.89.116:5601]

_As a **Bonus**, provide the specific commands the user will need to run to download the playbook, update the files, etc._