## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![ELK Stack Topology](https://github.com/lindseytwilson/Project-1/blob/main/Diagrams/ELK%20Stack%20Topology.png)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to recreate the entire deployment pictured above. Alternatively, select portions of the yml and config file may be used to install only certain pieces of it, such as Filebeat.

  - [Ansible Playbooks & Configuration Files](https://github.com/lindseytwilson/Project-1/tree/main/Ansible)

This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly available, in addition to restricting traffic to the network.
- What aspect of security do load balancers protect?
	- Load balancers help defend against denial-of-service attacks by shifting traffic to another web server if one goes down.
- What is the advantage of a jump box?_
	- Increased security, controlled access and separation between user's workstations and assets within the network.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the log and system files.
- What does Filebeat watch for?
	- Filebeat monitors log files and log events and sends the information to Elasticsearch or Logstash for indexing.
- What does Metricbeat record?
	- Metricbeat records the metrics and statistics from the operating system and services running on the server.

The configuration details of each machine may be found below.

| Name      | Function | IP Address | Operating System |
|-----------|----------|------------|------------------|
| JumpBox   | Gateway  | 10.0.0.4   | Linux            |
| Web1      | Client   | 10.0.0.5   | Linux            |
| Web2      | Client   | 10.0.0.6   | Linux            |
| Web3      | Client   | 10.0.0.7   | Linux            |
| ELK Server| Server   | 10.1.0.4   | Linux            |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the ELK Server machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- Whitelisted IP addresses: Host machine public IP address

Machines within the network can only be accessed by the host machine and JumpBox.
- Which machine did you allow to access your ELK VM? What was its IP address?
	- Host Machine via port 5601
	- JumpBox via 10.0.0.4:22

A summary of the access policies in place can be found in the table below.

| Name      | Publicly Accessible | Allowed IP Addresses          |
|-----------|---------------------|-------------------------------|
| JumpBox   | Yes                 | Host machine public IP via SSH|
| Web1      | No                  | 10.0.0.4                      |
| Web2      | No                  | 10.0.0.4                      |
| Web3      | No                  | 10.0.0.4                      |
| ELK Server| No                  | 10.0.0.4                      |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because is is flexible, agentless, and efficient. Ansible allows you to arrange an entire application environment no matter where it is deployed and it can also be customized based on your needs. You also don't need to set up a separate management structure, and you don't need to install any extra software. Lastly, no custom code is needed to automate the systems.

The playbook implements the following tasks:
- Specify the elk machines and RedAdmin user
- Install docker.io, python3-pip, and docker
- Increase system memory
- Launch the docker elk container with the following exposed ports: 5601, 9200, 5044
- [Full Ansible Playbook](https://github.com/lindseytwilson/Project-1/blob/main/Ansible/ansible-playbook.yml)

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![TODO: Update the path with the name of your screenshot of docker ps output](https://github.com/lindseytwilson/Project-1/blob/main/Images/docker%20ps.png)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- Web1: 10.0.0.5
- Web2: 10.0.0.6
- Web3: 10.0.0.7

We have installed the following Beats on these machines:
- Filebeat and Metricbeat have been installed on:
	- Web1
	- Web2
	- Web3
	- ELK Server

These Beats allow us to collect the following information from each machine:
- Filebeat collects log events
	- [Example Filebeat Data]()
- Mectricbeat collects metrics and system statistics 
	- [Example Metricbeat Data]()
### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the playbook file to /etc/ansible.
- Update the hosts file to include each Web VMs IP addresses as follows:
	- 10.0.0.5 ansible_python_interpreter=/usr/bin/python3
	- 10.0.0.6 ansible_python_interpreter=/usr/bin/python3
	- 10.0.0.7 ansible_python_interpreter=/usr/bin/python3
- To run the playbook
	- Run: ansible-playbook playbook-name.yml
	- Navigate to RedAdmin@10.0.0.5
	- Run: curl localhost/setup.php (checks to see that the installation worked as expected)

- Which file is the playbook? Where do you copy it?
	- ansible-playbook.yml
	- This playbook file gets copied to the /etc/ansible directory
- Which file do you update to make Ansible run the playbook on a specific machine? How do I specify which machine to install the ELK server on versus which to install Filebeat on?
	- The hosts file is used update to make ansible run on a specific machine. You specify which machine to install the ELK server on by adding the ELK Server IP address.
- Which URL do you navigate to in order to check that the ELK server is running?
	- The public IP address on the ELK Server via port 5601 (138.91.155.137:5601)