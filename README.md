## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.
![ElkNetworkDiagram drawio](https://user-images.githubusercontent.com/99552635/153762828-2c9aafd8-8576-44d4-9316-93af963c70bc.png)


**Note**: The following image link needs to be updated. Replace `diagram_filename.png` with the name of your diagram image file.  

/Elk-Stack-Project/diagrams

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the "YML and config" file may be used to install only certain pieces of it, such as Filebeat.

/Elk-Stack-Project/ansible/install-elk.yml
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

What aspect of security do load balancers protect? 
Performance and availability against denial-of-service (DDoS) attacks.  

What is the advantage of a jump box?
It is a more hardened and secure server that is launched and then connected to other servers, to provide an additional layer of security. The advantages to this are: network segmentation, access control, and automation.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the data and system logs.
- What does Filebeat watch for?
- Filebeat is used for forwarding and centralizing log data. It watches the log files or locations that you specify, collects log events, and forwards the either to Elasticsearch or Logstash for indexing.
- What does Metricbeat record?
- Metricbeat records the metrics and statistics that it collects and ships them to the specified output, such as Elasticsearch or Logstash. It monitors your servers by collecting metrics from the syste, and services running on the server, such as Apache.

The configuration details of each machine may be found below.
_Note: Use the [Markdown Table Generator](http://www.tablesgenerator.com/markdown_tables) to add/remove values from the table_.

| Name         | Function                                           | IP Address               | Operating System |
|----------    |----------                                          |-----------              -|------------------|
| Jump Box     | Gateway                                            | 10.0.0.4; 20.121.208.201 | Linux            |
| Web 1        | Webserver                                          | 10.0.0.7                 | Linux            |
| Web 2        | Webserver                                          | 10.0.0.6                 | Linux            |
| Web 3        | Webserver                                          | 10.0.0.9                 | Linux            |
| Elk Server   | Elk Server (centralized logging and monitoring)    | 10.1.0.4;  104.40.73.49  | Linux            |
| Load Balancer| Traffic distribution and balance                   | 52.186.121.85            | Linux            |
| Workstation  | Access Control                                     | Public IP of the workstation | Linux        |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Elk Server machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- Workstation public IP which can be found using google search: "what is my IP".

Machines within the network can only be accessed by Jumpbox provisioner, which is launched and accessed by the workstation machine.

A summary of the access policies in place can be found in the table below.

| Name               | Publicly Accessible | Allowed IP Addresses    |
|----------          |---------------------|----------------------   |
| Jump Box           | No                  | 10.0.0.4; 20.121.208.201|
| Load Balancer      | No                  | Workstation Public IP   |
| Web 1              | No                  | 10.0.0.7                |
| Web 2              | No                  | 10.0.0.6                |
| Web 3              | No                  | 10.0.0.9                |
| Elk Server         | No                  | Workstation Public IP   |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
- Ansible automation helps with representation of Infrastructure as Code (IAC). IAC involves provisioning, configiration management, deploying applications, security and compliance through machine-processable definition files. In simpler terms, with ansible, administrators can collaborate with developers which in turn improves efficiency and speed by focusing more on performance tuning rather than fixing issues in files. 

The playbook implements the following tasks:
- Specify a new machine (Elk Server) and new remote user (azadmin) 
<img width="248" alt="image" src="https://user-images.githubusercontent.com/99552635/153770534-3872f337-b8d5-4f0a-ac66-1aaf60f40f25.png">
- Increase system memory:
- <img width="188" alt="image" src="https://user-images.githubusercontent.com/99552635/153770585-f8094c93-87d5-4a2e-8f24-dbcf8bd88725.png">
- Install different services: docker.io, python3-pip, docker 
- Launch and expose the elk container by these published-ports: 
- <img width="371" alt="image" src="https://user-images.githubusercontent.com/99552635/153770702-b21dc0db-0885-4b93-bdbd-a635ab4133cc.png">

- 
The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

**Note**: The following image link needs to be updated. Replace `docker_ps_output.png` with the name of your screenshot image file.  


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
