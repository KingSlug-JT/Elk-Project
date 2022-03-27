## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![](Images/diagram_filename.png)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the _____ file may be used to install only certain pieces of it, such as Filebeat.

  - [filebeat-config.yml](Ansible/filebeat-config.yml)
  - [filebeat-playbook.yml](Ansible/filebeat-playbook.yml)
  - [metricbeat-config.yml](Ansible/metricbeat-config.yml)
  - [metricbeat-playbook.yml](Ansible/metricbeat-playbook.yml)

This document contains the following details:
- Description of the Topologu
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly available, in addition to restricting access to the network. The jump box in this setup provides on point of entry and exit giving a choke point for securing and configuring the internal network from the Internet.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the network and system configuration.

The configuration details of each machine may be found below.
_Note: Use the [Markdown Table Generator](http://www.tablesgenerator.com/markdown_tables) to add/remove values from the table_.

| Name       | Function                   | IP Address | Operating System     |
|------------|----------------------------|------------|----------------------|
| Jump Box   | Gateway                    | 10.1.0.4   | Linux (ubuntu 18.04) |
| Web-1      | Traffic Monitoring         | 10.1.0.7   | Linux (ubuntu 18.04) |
| Web-2      | Traffic monitoring         | 10.1.0.8   | Linux (ubuntu 18.04) |
| Elk Server | Data Analytics Generation  | 10.2.0.4   | Linux (ubuntu 18.04) |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the jumpbox/ Provisioner machine can accept connections from the Internet. Access to this machine is only allowed from the whitelisted public world IP address for the admin through ssh(port22).  

Machines within the network can only be accessed by jumpbox/ provisioner within itsansible container @ 10.1.0.4

A summary of the access policies in place can be found in the table below.

| Name       | Publicly Accessible | Allowed IP Addresses    |
|------------|---------------------|-------------------------|
| Jump Box   | Yes                 | SSh from Whitelisted Ip |
| Web-1      | No                  |                         |
| Web-2      | No                  |                         |
| Elk Server | Yes                 | SSH from Whitelisted Ip |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because this reduces deployment time per container, allowing for scalable dployment and eliminates manual configuration and errors.

The playbook implements the following tasks:
- Installs the following modules within the container: docker.io, pip3, Install Docker python module
- Configures sysctl modules
- Sets the docker services to boot on docker start

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![docker ps output](Images/Elk_dockerPs.png)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- Web-1 10.1.0.7
- Web-2 10.1.0.8

We have installed the following Beats on these machines:
- FileBeat version 7.6.2
- MetricBeat version 7.6.2

These Beats allow us to collect the following information from each machine:
- Filebeat is a lightweight shipper that fowards and centralizes logs and files.
- Metricbeat is a lightweight shipper that collects data from the operating system and running services.

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the filebeat.config and metricbeat.config files to the ansible container /etc/ansible/roles
- Update the configuration files to include correct IP addresses of the local IP addresses for the elk server @ 10.2.0.4:5601 and 10.2.0.4:9200 
- Run the filebeat and metricbeat playbooks, and navigate to kibana server with the ip pf elk server to check that the installation worked as expected.

_TODO: Answer the following questions to fill in the blanks:_
- The playbooks are (Ansible/filebeat-playbook.yml) and (Ansible/metricbeat-playbook.yml) you will need to copy these files over to the ansible roles directory on the ansible container.
- You will need to update the filebeat-config.yml and metricbeat-config.yml on lines 1106 and 1806 to add the elk private IP addess so that the deployment modules are deployed corecctly.
- To navigate to the elk server use web address http://<public elk ip>:5601/app/kibana#/home


