## Automated ELK Stack Deployment

The files in this repository were used to configure the ELK component of the virtual network depicted below:

https://github.com/RyanCCary/DU_Cyber_Project_1/blob/main/Diagrams/Cary_DU_Cyber_Network_Diagram_final.PNG

The following "install-elk.yml" file has been tested and used to generate a live ELK deployment on Azure; it can likewise be used to recreate the deployment pictured above:

 https://github.com/RyanCCary/DU_Cyber_Project_1/blob/main/Ansible/ELK_configuration_Ansible_YAML_playbook_example.txt

Alternatively, select portions of the playbook file ("install-elk.yml", in this case) may be used to install only specific pieces of it, such as Filebeat, as illustrated by this example:

 https://github.com/RyanCCary/DU_Cyber_Project_1/blob/main/Ansible/ELK_Filebeat_configuration_YAML_example.txt

This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build

### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly available, in addition to restricting malicious access to the network. Load balancers protect against denial or service attacks, as well as enable additional network security rules to resist other malicious traffic attempting to reach application servers.

These servers can be further hardened by using an SSH-connected "jump server" to manage them via Ansible (host) and Docker (client) containers, reducing the web servers' surface of attack through other ports or alternate administrative mechanisms.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the configurations and system operation.

The configuration details of each machine may be found below.
## _Note: Use the [Markdown Table Generator](http://www.tablesgenerator.com/markdown_tables) to add/remove values from the table_.

| Name     | Function |  IP Address   | Operating System |
|----------|----------|---------------|------------------|
| Jump Box | Gateway  | 52.233.74.138 | Linux            |
| WebSrvr1 | App Srvr | 10.0.0.9      | Linux            |
| WebSrvr3 | App Srvr | 10.0.0.12     | Linux            |
| ELKVM1   | Security | 52.184.196.156| Linux            |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

The jump server can accept SSH connections, and web servers' load balancer can accept connections from the administrator's private IP address.

Machines within the network can be accessed by the jump server via SSH; additionally, the ELK server and web servers may be accessed from the adminstrator's private IP address.

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------|
| Jump Box | No                  | SSH                  |
| WebSrvr1 | No                  | Administrator IP     |
| WebSrvr3 | No                  | Administrator IP     |
| ELKVM1   | No                  | Administrator IP     |

### ELK Configuration

Ansible was used to automate configuration of the ELK machine. Avoiding manual configuration saves time, provides an automated status / confirmation of installation, and enables a simple repeatable update process moving forward.

The "install-elk.yml" playbook implements the following tasks:
- Installs the Docker application and Python3 translator and Ansible module to correctly configure it.
- Uses additional Ansible modules to increase the ELK VM's virtual memory.
- Downloads and launches the ELK docker container and commands it to start each time the VM boots.

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance:
https://github.com/RyanCCary/DU_Cyber_Project_1/blob/main/Ansible/Successfully_configured_ELK_Docker.PNG

The ELK server is also configured to communicate specifically through port 5601, enforced by an incoming firewall rule.

### Target Machines & Beats
This ELK server is configured to monitor the following machines:

| Name     | Function |  IP Address   | Operating System |
|----------|----------|---------------|------------------|
| WebSrvr1 | App Srvr | 10.0.0.9      | Linux            |
| WebSrvr3 | App Srvr | 10.0.0.12     | Linux            |

The install of Filebeat and Metricbeat on both of these machines allows best-in-class log monitoring and data transformation for analysis. Per Elastic's product description, "Filebeat monitors the log files or locations that you specify, collects log events, and forwards them either to Elasticsearch or Logstash for indexing." Metricbeat "takes the metrics and statistics that it collects and ships them to the output that you specify, such as Elasticsearch or Logstash."

### Using the Playbook
In order to use the playbook, an admin may do the following, using the correctly configured Ansible control node: 

SSH into the control node and follow the steps below:
- Copy the install-elk.yml file to the /etc/ansible/files/ directory.
- Update the /etc/ansible/hosts file to include an ELK category that contains the IP of the ELK VM.
- Run the playbook with the "ansible-playbook install-elk.yml" command; this command will also update the system configuration when used following updates to the playbook.
- Navigating to http://137.116.75.136:5601/app/kibana will check that the installation worked as expected.
