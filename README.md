# cybersec-class
Projects from my class

## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

 [Cloud Security Diagram](./Diagrams/Cloud_Security_Unit.png)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the _____ file may be used to install only certain pieces of it, such as Filebeat.

 [Filebeat YAML File](./Ansible/filebeat-playbook.yml)

This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the Damn Vulnerable Web Application.

Load balancing ensures that the application will be highly available, in addition to restricting traffic to the network.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the logs and system metrics.

The configuration details of each machine may be found below.

| Name     | Function                     | IP Address | Operating System       |
| -------- | ---------------------------- | ---------- | ---------------------- |
| Jump Box | Gateway                      | 10.0.0.4   | Linux Ubuntu 18.04 LTS |
| Web1     | Webserver for DVWA           | 10.0.0.5   | Linux Ubuntu 18.04 LTS |
| Web2     | Redundant webserver for DVWA | 10.0.0.6   | Linux Ubuntu 18.04 LTS |
| ELK      | Webserver to run Kibana      | 10.1.0.4   | Linux Ubuntu 18.04 LTS |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Load Balancer and ELK machines can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses: 52.186.140.158, 52.229.115.199

Machines within the network can only be accessed by Jumpbox.

A summary of the access policies in place can be found in the table below.

| Name                        | Publicly Accessible | Allowed IP Addresses |
| --------------------------- | ------------------- | -------------------- |
| Jump Box VM                 | Yes                 | 40.117.225.10        |
| Web1 and Web2 Load Balancer | Yes                 | 52.186.140.158       |
| ELK VM                      | Yes                 | 52.229.115.199       |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
You don't have to configure each machine manually and you can define one set of installation and config files.

The playbook implements the following tasks:
- Define the Host
- Become Root
- Install Docker
- Install Python
- Install Docker Module
- Increase Container Memory
- Download and launch a docker elk container
- Define ports that Elk runs on.

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

[Docker PS output image](Images/docker_ps_output.png)

### Target Machines & Beats
This ELK server is configured to monitor the following machines: Web1 10.0.0.5 and Web2 10.0.0.6

We have installed the following Beats on these machines: Filebeat and Metricbeats

These Beats allow us to collect the following information from each machine:
  - Filebeat collects systemd logs and forwards them to ELK
  - Metricbeats collects all Docker container metric data and send it to ELK 

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the filebeat-playbook.yml file to /etc/ansible/roles

- Update the hosts file to include...:

  - [webservers]

    10.0.0.5 ansible_python_interpreter=/usr/bin/python3
    10.0.0.6 ansible_python_interpreter=/usr/bin/python3

    [elk]
    10.1.0.4 ansible_python_interpreter=/usr/bin/python3

- Run the playbook, and navigate to 52.229.115.199:5601 to check that the installation worked as expected.

