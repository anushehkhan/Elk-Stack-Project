## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.
!<img width="904" alt="image" src="https://user-images.githubusercontent.com/99552635/153776984-6d4eb443-eda9-49c4-9e1f-c84e51dd0aeb.png">


[Network Diagram](https://github.com/anushehkhan/Elk-Stack-Project/blob/main/diagrams/ElkNetworkDiagram.drawio.png)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the "YML and config" file may be used to install only certain pieces of it, such as Filebeat.

- [Ansible ELK installation and VM Config](https://github.com/anushehkhan/Elk-Stack-Project/blob/main/ansible/install-elk.yml)
- [Ansible Hosts](https://github.com/anushehkhan/Elk-Stack-Project/blob/main/ansible/hosts)
- [Ansible Configuration](https://github.com/anushehkhan/Elk-Stack-Project/blob/main/ansible/ansible.cfg)
- [Ansible Filebeat Playbook](https://github.com/anushehkhan/Elk-Stack-Project/blob/main/ansible/filebeat-playbook.yml)
- [Ansible Metricbeat Playbook](https://github.com/anushehkhan/Elk-Stack-Project/blob/main/ansible/metricbeat-playbook.yml)

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
Filebeat is used for forwarding and centralizing log data. It watches the log files or locations that you specify, collects log events, and forwards the either to Elasticsearch or Logstash for indexing.
- What does Metricbeat record?
Metricbeat records the metrics and statistics that it collects and ships them to the specified output, such as Elasticsearch or Logstash. It monitors your servers by collecting metrics from the syste, and services running on the server, such as Apache.

The configuration details of each machine may be found below.
_Note: Use the [Markdown Table Generator](http://www.tablesgenerator.com/markdown_tables) to add/remove values from the table_.

| Name| Function| IP Address| Operating System|
|----------|---------- |------------|------------------|
| Jump Box| Gateway | 10.0.0.4; 20.121.208.201 | Linux |
| Web 1 | Webserver| 10.0.0.7| Linux |
| Web 2| Webserver | 10.0.0.6 | Linux |
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
<img width="188" alt="image" src="https://user-images.githubusercontent.com/99552635/153770585-f8094c93-87d5-4a2e-8f24-dbcf8bd88725.png">
- Install different services: docker.io, python3-pip, docker 

- Launch and expose the elk container by these published-ports: 
<img width="371" alt="image" src="https://user-images.githubusercontent.com/99552635/153770702-b21dc0db-0885-4b93-bdbd-a635ab4133cc.png">

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.
<img width="785" alt="image" src="https://user-images.githubusercontent.com/99552635/153771533-2efb3090-4353-4c25-9968-7304e4d6a05e.png">

**Note**: The following image link needs to be updated. Replace `docker_ps_output.png` with the name of your screenshot image file.  
(/Images/dockerps.png)

NOTE: Status of Web servers 1-3 ran and screenshots uploaded in the images directory.

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
-Web 1: 10.0.0.7
-Web 2: 10.0.0.6
-Web 3: 10.0.0.9

We have installed the following Beats on these machines:
- FileBeat and MetricBeat

These Beats allow us to collect the following information from each machine:
- Filebeat: log events
- Metricbeat: system statistics and metrics

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:

- Copy the install-elk.yml file to docker container (in the /etc/ansible directory). Run the playbook: ansible-playbook install-elk.yml. This is the playbook used to install and configure elk container.

- Update the filebeat-playbook.yml to include installer
curl -L -O https://artifacts.elastic.co/downloads/beats/filebeat/filebeat-7.6.1-amd64.deand 
Update the metricbeat-playbook.yml files to include installer
curl -L -O https://artifacts.elastic.co/downloads/beats/metricbeat/metricbeat-7.6.1-amd64.deb
**The metricbeat-playbook.yml and filebeat-playbook.yml are the two playbooks for metricbeat and filebeat, and we copy those in the docker container.

- Update the filebeat-config.yml and metricbeat-config.yml files to include private IP address of the ELK server in elasticsearch and kibana output as shown below.
<img width="596" alt="Edit-filebeat-config yml" src="https://user-images.githubusercontent.com/99552635/153773937-920122d7-9726-4b83-9cb0-6bde077047d2.png">
<img width="707" alt="image" src="https://user-images.githubusercontent.com/99552635/153774022-a11eba82-6710-4c56-9b42-44c9d5c4b659.png">
**The ansible Hosts file in the /etc/ansible/hosts directory is confirguered to run the playbook on specific machines. The private IP addresses are written into these files to specify which machines to install the ELK server on. [webservers] and [elk] are groups. When you run playbooks with Ansible, you specify which group to run them on. This allows you to run certain playbooks on some machines, but not on others. <img width="400" alt="image" src="https://user-images.githubusercontent.com/99552635/153775955-d589020d-a474-404e-8ea3-f9eca395a1dc.png">

- Run the playbooks using these commands: (ansible-playbook filebeat-playbook.yml) (ansible-playbook metricbeat-playbook.yml), and navigate to Kibana to check that the installation worked as expected.


_As a **Bonus**, provide the specific commands the user will need to run to download the playbook, update the files, etc.

NOTE: Bonus commands are in images folder. The names of the images describes what each command is performing.

## Additional Notes

**To get Log Data:** To get Log data from Kibana: Enter url http://[public-ip-elk-server]:5601/app/kibana#home > Click Logs > Click Add log data > System logs > Click check data > Systems Log Dashboard

**To get Metrics Data:** To get metrics data from Kibana: Enter url http://[public-ip-elk-server]:5601/app/kibana#home > Add Metric Data > Docker Metrics > Check Data > Docker Metrics Dashboard

**To download and create Filebeat playbook:** Enter command in your docker container: curl -L -O https://artifacts.elastic.co/downloads/beats/filebeat/filebeat-7.6.1-amd64.deb > filebeat-playbook.yml

**To download and create Metricbeat playbook:** Enter command in your docker container: curl -L -O https://artifacts.elastic.co/downloads/beats/metricbeat/metricbeat-7.6.1-amd64.deb > metricbeat-playbook.yml

**To update ansible configuration file:** Enter command: nano /etc/ansible/hosts and add the IP addresses for the webservers and elk server as shown in picture above.


**Other useful commands:**

**sudo apt-get update**: updates all packages

**sudo apt install docker.io**: installs docker application

**sudo service docker start**: starts the docker application

**systemctl status docker**: shows the status of the docker application (if it is running)

**sudo docker pull cyberxsecurity/ansible**: Downloads the docker file

**sudo docker run -ti cyberxsecurity/ansible bash**: RUns and creates a docker image

**sudo docker start [insert docker image name]** : starts the image 

**sudo docker ps -a** : lists active or inactive containers

**sudo docker attach [insert docker image name]** : ssh into the ansible container

**ssh-keygen**: creates an ssh key
