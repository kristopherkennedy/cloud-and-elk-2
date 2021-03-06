# cloud-and-elk-2
## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![Diagram](https://github.com/kristopherkennedy/cloud-and-elk-2/blob/main/azure%20diagram%20resource%20groups.png)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the _____ file may be used to install only certain pieces of it, such as Filebeat.

  -   [Ansible Configuration](Ansible/playbooks/ansible.cfg)
  -   [Ansible Playbook](Ansible/playbooks/elk-playbook)
  -   [Filebeat Config](Ansible/playbooks/filebeat-config.yml)
  -   [Filebeat Playbook](Ansible/playbooks/filebeat-playbook.yml.txt)
  -   [Metricbeat Config](Ansible/playbooks/metricbeat.config)
  -   [Metricbeat Playbook](Ansible/playbooks/metricbeat-playbook.yml)
  -   

This document contains the following details:
- Description of the Topologu
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly Avaolable, in addition to restricting inbound access to the network.
-  What aspect of security do load balancers protect? What is the advantage of a jump box?_

a load balancer will assist in monitoring and directing traffic. it can also identify if a server is in need of maintnance or not responding due to being offline

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the file system of the VMs on the network and system metric_.
-  What does Filebeat watch for?

Filebeat organizes file system log files and send this information to logstash and elasticsearch to help put into human read-able form
-  What does Metricbeat record?

Similar to filebeat metricbeat collects operating system services and send the information to logstash and elasticsearch to be broken into human read-able form

The configuration details of each machine may be found below.
_Note: Use the [Markdown Table Generator](http://www.tablesgenerator.com/markdown_tables) to add/remove values from the table_.

| Name     | Function |       IP Address         | Operating System |
|----------|----------|--------------------------|------------------|
| Jump Box | Gateway  | 10.0.0.1/104.43.251.20   | Linux            |
| DVWA     |webserver | 10.0.0.5/40.122.33.239   | Linux            |
| DVWA     |webserver | 10.0.0.6/40.122.33.239   | Linux            |
| ELK      |monitoring| 10.1.0.4/157.55.164.105  | Linux            |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the jummpbox machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- Add whitelisted IP addresses?_
Public ip with TCP 5601

Machines within the network can only be accessed by _____.
- Which machine did you allow to access your ELK VM? What was its IP address?_
jump box - (private) 10.0.0.4, (public) 104.43.251.20
local machine - (public) 76.187.11.37 
A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------|
| Jump Box | Yes                 |ssh(22)local public ip|
|  web-1   | no                  |ssh(22)10.0.0.5       |
|  web-2   | no                  |ssh(22)10.0.0.6       |
|  Elk     | no                  |ssh(22)10.1.0.4 & local public ip

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
- What is the main advantage of automating configuration with Ansible?_
it allows you to create a cripts that will run muliple tasks at once without having to enter manually which saves time and resorces

The playbook implements the following tasks:
- the ansible header can specify a different group of machines as well as different remote users
- the playbook will install docker.io, python3-pip,cocker
- the container will be startd with ports (5601,9200,5044) 
- we also increased the memory to 262144

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![docker](docker_ps_output.png.png)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- List the IP addresses of the machines you are monitoring_
web-1 10.0.0.5
web-2 10.0.0.6
We have installed the following Beats on these machines:
- Specify which Beats you successfully installed_
Filebeat
Metricbeat

These Beats allow us to collect the following information from each machine:
- In 1-2 sentences, explain what kind of data each beat collects, and provide 1 example of what you expect to see. E.g., `Winlogbeat` collects Windows logs, which we use to track user logon events, etc._
Filebeat forwards centralized log data from a server. it uses the following tool to monitor data (NGINX, MySQL, Auditd)
Metricbeat collects operating system metrics and services running on a server by focusing on the systems CPU memory and load
### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the Install Elk file to Ansible.
- Update the /etc/ansible/hosts file to include VM ip address (10.1.0.4)
- Run the playbook, and navigate to "Http://YourIPAddress:5601/app/kibana" to check that the installation worked as expected.

_ Answer the following questions to fill in the blanks:_
- _Which file is the playbook? Where do you copy it?_

ansible-playbook install-elk.yml
- _Which file do you update to make Ansible run the playbook on a specific machine? How do I specify which machine to install the ELK server on versus which to install Filebeat on?_

you update the hosts file
you seperate the [webserver] 10.0.0.5 & 10.0.0.6 private ip addresses and the [elk] server 10.1.0.4 private ip adresss
- _Which URL do you navigate to in order to check that the ELK server is running?_

you navigate to the http://[your.vm.ip];5601/app/kibana
 
