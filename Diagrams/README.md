## University of Denver Cybersecurity Diagrams

What follows are diagrams and descriptions of systems I built or managed as part of my work in the University of Denver Cybersecurity program in early 2021.

### Description of My Azure Virtual Network Topology

This is a diagram of the virtual network I built for the University of Denver Cybersecurity program: https://github.com/RyanCCary/DU_Cyber_Project_1/blob/main/Diagrams/Cary_DU_Cyber_Network_Diagram_final.PNG

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly available, in addition to restricting malicious access to the network. Load balancers protect against denial or service attacks, as well as enable additional network security rules to resist other malicious traffic attempting to reach application servers.

These servers can be further hardened by using an SSH-connected "jump server" to manage them via Ansible (host) and Docker (client) containers, reducing the web servers' surface of attack through other ports or alternate administrative mechanisms.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the configurations and system operation.

Additional details on integrated applications, security, and management practices may be found in the Ansible section of this repository.