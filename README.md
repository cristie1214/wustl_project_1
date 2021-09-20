## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

[Diagrams/Red Team Cloud Network Diagram.drawio.png](https://github.com/cristie1214/wustl_project_1/blob/994722b1424131d379db4c4cfa926772b2274582/Diagrams/Red%20Team%20Cloud%20Network%20Diagram.drawio.png)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the YML file may be used to install only certain pieces of it, such as Filebeat.

  - [Ansible/elk.yml](https://github.com/cristie1214/wustl_project_1/blob/56fb129b66beb90f3f01c3af32fed96511a8cbc5/Ansible/elk.yml)
  - [Ansible/filebeat.-playbook.yml](https://github.com/cristie1214/wustl_project_1/blob/56fb129b66beb90f3f01c3af32fed96511a8cbc5/Ansible/filebeat.-playbook.yml)
  - [Ansible/metricbeat-playbook.yml](https://github.com/cristie1214/wustl_project_1/blob/56fb129b66beb90f3f01c3af32fed96511a8cbc5/Ansible/metricbeat-playbook.yml)

This document contains the following details:
- Description of the Topologu
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly efficient, in addition to restricting high-traffic to the network.
- Load Balancers manage the flow of traffic between the server and the endpoint to prevent server overloading which ensures accessability and helps prevent DDos attacks.   The advantage of a jump box is so that IT administrators can have controlled access between networks.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the network and system logs.
- Filebeat watches for log files that you specify, collects the log events, and then forwards them to Elasticsearch or Logstash for indexing.
- Metricbeat records the metrics and statistics and shipd them to either Elasticsearch or Logstash.

The configuration details of each machine may be found below.
_Note: Use the [Markdown Table Generator](http://www.tablesgenerator.com/markdown_tables) to add/remove values from the table_.

| Name     | Function | IP Address | Operating System |
|----------|----------|------------|------------------|
| Jump Box | Gateway  | 10.0.0.4   | Linux            |
| Web 1    | webserver| 10.0.0.5   | Linux            |
| Web 2    | webserver| 10.0.0.7   | Linux            |
| Elk VM   | webserver| 10.1.0.4   | Linux            |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jump Box machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- 40.76.227.8

Machines within the network can only be accessed by Jump Box.
- The Jump Box is the machine allowed to access the Elk VM.  The Jump Box IP address is 10.0.0.4

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------|
| Jump Box | Yes                 | 40.76.227.8          |
| Web 1    | No                  | 10.0.0.4             |
| Web 2    | No                  | 10.0.0.4             |
| Elk VM   | No                  | 10.0.0.4             |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because it is simple to set up and use. 
-The main advantage of Ansible is the use of YAML playbooks to automate, configure, deploy, and orchestrate the IT infrastructure.

The playbook implements the following tasks:

- An Elk VM needs to be created and docker installed
- Add the Elk VM to the host file and create a new playbook for the Elk machine
- Download and run elk to launch the Elk container
- SSH into the Elk container and verify it is running

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

[Diagrams/Docker ps.jpg](https://github.com/cristie1214/wustl_project_1/blob/efe2668c09f823be080c23cd5f70df5a873fbac2/Diagrams/Docker%20ps.jpg)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- Web-1 (10.0.0.5)
- Web-2 (10.0.0.7)

We have installed the following Beats on these machines:
- Filebeat
- Metricbeat

These Beats allow us to collect the following information from each machine:
-Filebeat collects log data such as server logs, audit logs, depreciation logs, etc. that can be reviewed and analyzed. Metricbeat collects metric data from target servers such as CPU usage and memory metrics.

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the filebeat-configuration.yml file to /etc/ansible/files
- Update the filebeat-configuration.yml file to include the Elk private IP address in lines 1106 and 1806.
- Run the playbook, and navigate to URL 20.94.248.50:5601 to check that the installation worked as expected.

_TODO: Answer the following questions to fill in the blanks:_
- filebeat-playbook.yml is the playbook file that is copied /etc/ansible/
- You will update the host file with the IP addresses of the virtual machines you want Ansible to run the playbook on.  Within the host file there are webservers listed that can be specified to Filebeat and Elk servers that Elk would be installed on. 
- In order to ensure the Elk server is running you would navigate to URL 20.94.248.50:5601 

**Bonus:** The commands needed to download the playbook, update the files, etc. are:
 - ssh into your ansible container and start docker docker start *container name* (if not on machine install docker: apt install docker)
 - create a filebeat-config.yml in your container using nano filebeat-config.yml 
 - a filebeat-playbook.yml would then be created also using nano filebeat-playbook.yml
 - to run the playbook you use the absolute path or run from the directory the playbook is located in with the command: ansible-playbook filebeat-playbook.yml
