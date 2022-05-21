## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

[Images/RTdiagram.png](https://github.com/emadans/Project-1/blob/c52972a2f5cc25566aa7a3c1404d84690eb73be1/README/Images/RTdiagram.png)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the playbook file may be used to install only certain pieces of it, such as Filebeat.

  - [Playbooks/install_elk_ymlplaybook.yml](https://github.com/emadans/Project-1/blob/db7119e3960792334c579c00d44d4f4494394bb1/README/Playbooks/install_elk_ymlplaybook.yml)
  - [Playbooks/install_filebeat_ymlplaybook.yml](https://github.com/emadans/Project-1/blob/db7119e3960792334c579c00d44d4f4494394bb1/README/Playbooks/install_filebeat_ymlplaybook.yml)
  - [Playbooks/install_metricbeat_ymlplaybook.yml](https://github.com/emadans/Project-1/blob/db7119e3960792334c579c00d44d4f4494394bb1/README/Playbooks/install_metricbeat_ymlplaybook.yml)
  - [Playbooks/setup_DVWA_ymlplaybook.yml](https://github.com/emadans/Project-1/blob/db7119e3960792334c579c00d44d4f4494394bb1/README/Playbooks/setup_DVWA_ymlplaybook.yml)

This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly redundant, in addition to restricting access to the network.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the log data and system services.

The configuration details of each machine may be found below.
_Note: Use the [Markdown Table Generator](http://www.tablesgenerator.com/markdown_tables) to add/remove values from the table_.

| Name       | Function                  | IP Address | Operating System |
|------------|---------------------------|------------|------------------|
| JumpBox    | Gateway                   | 10.0.0.4   | Linux            |
| Web1       | Web Server                | 10.0.0.5   | Linux            |
| Web2       | Web Server                | 10.0.0.6   | Linux            |
| ELK Server | Monitor Logs and Services | 10.1.0.4   | Linux            |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the JumpBox machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses: 23.123.149.165

Machines within the network can only be accessed by JumpBox with the IP address 10.0.0.4.  The ELK VM will accept SSH from any IP address, but will only accept traffic on Port 5601 from my IP address, 23.123.149.165.  This makes Kibana only accessible from my IP address.  

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------|
| Jump Box | Yes                 | 23.123.149.165       |
| Web1     | No                  | 10.0.0.4             |
| Web2     | No                  | 10.0.0.4             |
| ELK      | Yes                 | 23.123.149.165       |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because it can be installed on multiple machines with one command.  

The playbook implements the following tasks:
- Install Docker (docker.io) on the ELK VM
- Install Python (python3-pip) on the ELK VM
- Instruct Docker to default to Python
- Increase virtual memory of ELK server
- Download and Launch an ELK container on our ELK VM using docker_container

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

[Images/docker_ps_output.png](https://github.com/emadans/Project-1/blob/db7119e3960792334c579c00d44d4f4494394bb1/README/Images/docker_ps_output.png)

### Target Machines & Beats
This ELK server is configured to monitor the following machines: 
- Web1 (Private IP: 10.0.0.5 Public IP of Load Balancer: 20.248.196.71) 
- Web2 (Private IP: 10.0.0.6 Public IP of Load Balancer: 20.248.196.71) 

We have installed the following Beats on these machines:
- Metricbeat
- Filebeat

These Beats allow us to collect the following information from each machine:
- Metricbeat monitors your operating system and services on your server, such as Apache.  
- Filebeat monitors all the log data on your server.  Any changes in the /var/log directory would reflect in Kibana.

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the install_elk_ymlplaybook.rtf file to the /etc/ansible directory.
- Update the hosts file to include the IP address of the machine you would like to install this on under the header [elk].  
- Run the playbook, and navigate to http://[your.ELK-VM.External.IP]:5601/app/kibana to check that the installation worked as expected.
