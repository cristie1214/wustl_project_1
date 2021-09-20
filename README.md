## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

Diagrams/Red Team Cloud Network Diagram.drawio.png

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the YML file may be used to install only certain pieces of it, such as Filebeat.

  - _TODO: Enter the playbook file._

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
- Filebeat watches for log fiels that you specify, collects the log events, and then forwards them to Elesticsearch or Logstash for indexing.
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
- The Jumo Box is the machine allowed to access the Elk VM.  The Jump Box IP address is 10.0.0.4

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

- An Elk VM needs to be created 
- Add the Elk VM to the host file and create a new playbook for the Elk machine
- Download and run elk to launch the Elk container
- SSH into the Elk container and verify it is running

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![TODO: Update the path with the name of your screenshot of docker ps output](Images/docker_ps_output.png)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- Web-1 (10.0.0.5)
- Web-2 (10.0.0.7)

We have installed the following Beats on these machines:
- Filebeat
- Metricbeat

These Beats allow us to collect the following information from each machine:
- _TODO: In 1-2 sentences, explain what kind of data each beat collects, and provide 1 example of what you expect to see. E.g., `Winlogbeat` collects Windows logs, which we use to track user logon events, etc._

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the filebeat-configuration.yml file to /etc/ansible/files
- Update the filebeat-configuration.yml file to include the Elk private IP address in lines 1106 and 1806.
- Run the playbook, and navigate to URL 20.94.248.50:5601 to check that the installation worked as expected.

_TODO: Answer the following questions to fill in the blanks:_
- filebeat-playbook.yml file to /etc/ansible/
-You will update the host file with the IP addresses of the virtual machines you want Ansible to run the playbook on.  Within the host file there are webservers listed that can be specified to Filebeat and Elk servers that Elk would be installed on. 
In order to ensure the Elk server is running you would navigate to URL 20.94.248.50:5601 

_As a **Bonus**, provide the specific commands the user will need to run to download the playbook, update the files, etc._
