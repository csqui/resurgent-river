# resurgent-river
## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below:

![Project1_NetworkDiagram drawio](https://user-images.githubusercontent.com/85413148/134089676-83753596-7bd7-4e94-a2bd-2d77029e9f04.png)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the beat-playbook.yml file may be used to install only certain pieces of it, such as Filebeat.


This document contains the following details:
- Description of the Topologu
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly efficient, in addition to restricting unauthorized access to the network.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to operating system metrics or log data.

The configuration details of each machine may be found below.

| Name     | Function       | IP Address | Operating System |
|----------|----------------|------------|------------------|
| Jump Box | Gateway        | 10.0.0.4   | Linux            |
| Web-1    | Webserver      | 10.0.0.5   | Linux            |
| Web-2    | Webserver      | 10.0.0.6   | Linux            |
| ElkVM1   | ELK stack host | 10.1.0.4   | Linux            |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the ElkVM1 machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses: 136.36.56.1

Machines within the network can only be accessed by a specific local machine (with an IP Address of 136.36.56.1).

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses            |
|----------|---------------------|---------------------------------|
| Jump Box | No                  | 10.0.0.5, 10.0.0.6, 136.36.56.1 |
| Web-1    | No                  | 10.0.0.4, 136.36.56.1           |
| Web-2    | No                  | 10.0.0.4, 136.36.56.1           |
| ElkVM1   | No                  | 136.36.56.1                     |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because if any additional machines or containers were added to the ELK network, they could be easily and identically configured.

The playbook implements the following tasks:
- Installs Docker
- Installs Python3-pip and a Docker phython module
- Downloads and launches a Docker web ELK container
- Increases and authorizes the use of sufficient virtual memory
- Enables Docker

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance:

![docker_ps_output](https://user-images.githubusercontent.com/85413148/134089674-da7fb7f6-8271-4a93-b1ba-5bb5d276400d.PNG)

### Target Machines & Beats
This ELK server is configured to monitor the following machines: 10.0.0.5 and 10.0.0.6

We have installed the following Beats on these machines: filebeat and metricbeat.

These Beats allow us to collect information from each machine. Filebeat collects log data and sends it to either Elasticsearch or Logstash where the logs are indexed and put in an easy to search and read format. We could expect to see log data specifying what activities have been done on a given machine. Metricbeat allows us to collect information about the metrics of the OS and send that information to Elasticsearch or Logstash as well, again where the data can be viewed easily. Metricbeat can be expected to show information about different operating systems and their status.


### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the beat-playbook.yml and install-elk.yml files to /etc/ansible.
- Update the hosts file to include IP addresses 10.0.0.5 and 10.0.0.6 under a group named [webservers] and the IP address 10.1.0.4 under a group named [elk]
- Run the playbooks, and navigate to http://<ElkVM1's Public IP Address>:5601/app/kibana to check that the installation worked as expected.
