## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

(Images/diagram_VirtualNetwork.png)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the yaml file may be used to install only certain pieces of it, such as Filebeat.

(Playbooks/install-elk.yml)
(Playbooks/filebeat-playbook.yml)

This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a monitored instance of DVWA, the D*mn Vulnerable Web Application.

The Jump Box serves as the gateway to the virtual network.  This allows the administrator the ability to have remote access capability.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the uptime and system logs.
- Filebeat is deployed on VMs in the environment in order to monitor all the system logs that are being generated. 

Future enhancements: Metricbeat and a Load balancer 

Although Metricbeat was not deployed for this current build it is certainly on the short list for furture enhancements.  Metricbeat records uptime and system metrics based around the VMs perfomrace related to the CPU, memory, etc.

If the pool of VMs begins to grow adding a load balancer will ensure that the application will be highly stable with the increased traffic.  The load balancer will also help keep the network's availability high with routing traffic evenly across the networks. 

The configuration details of each machine may be found below.

| Name     | Function | IP Address | Operating System |
|----------|----------|------------|------------------|
| Jump Box |Gateway   | 10.0.0.1   |Linux/Ubuntu 18.04|
| DVWA-VM1 |Filebeat  | 10.0.0.6   |Linux/Ubuntu 18.04|
| ELK      |ELK Server| 10.0.0.4   |Linux/Ubuntu 18.04|
|          |          |            |                  |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the ELK machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- 13.68.150.40

Machines within the network can only be accessed by Secure Shell (SSH).
- The Jump Box has acces to the ELK ELK VM. Its IP address is 13.68.151.203

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------|
| Jump Box | Yes                 | 10.0.0.5             |
| DVWA-VM1 | No                  |                      |
| ELK      | No                  |                      |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
- The main advantage of automating configuration with Ansible is that it can speed up the deployment of a virtual network.

The playbook implements the following tasks:
- Install docker.io
- Install python-pip
- Install docker module pip
- Increase virtual memory
- Downlaod and launch a docker elk container

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

(Images/docker_ps_output.png)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- 10.0.0.6

We have installed the following Beats on these machines:
- DVWA-VM1: Filebeat

This Beat allows us to collect the following information from the machine:
- This data collected using this beat can be from the syslog which can tell us what proccess started running and the time the process started.  The data can also show you what commands have been run as the root user.

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the yaml file to the host VM.
- Update the yaml file to include...
- Run the playbook, and navigate to host VM to check that the installation worked as expected.

Answer the following questions to fill in the blanks:
- Which file is the playbook? 
    The yaml(.yml) file is the playbook.
- Which file do you update to make Ansible run the playbook on a specific machine? 
    You must update the hosts file.
- How do I specify which machine to install the ELK server on versus which to install Filebeat on?
    In the heading of the yaml file next to host, specifify which machine you want to perform the install using the category you listed the machine on in the hosts file.
- Which URL do you navigate to in order to check that the ELK server is running?
    http://13.68.150.40:5601


