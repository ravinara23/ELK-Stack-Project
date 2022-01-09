# Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![Homework 12_ Cloud Security drawio](https://user-images.githubusercontent.com/89654192/148660768-7df65757-8cf5-4bbe-b509-37e5b13c7d8c.png)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the Playbook file may be used to install only certain pieces of it, such as Filebeat.
- Elk Playbook.yml
- Metricbeat.yml
- Filebeatplaybook.yml
- Myplaybook.yml


This document contains the following details:

- Description of the Topology
- Access Policies
- ELK Configuration
    - Beats in Use
    - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology
The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly available, in addition to restricting access to the network.
- Load Balancers protect against denial of service attacks (DDoS) because it analyzes the traffic thats coming in and can send traffic to particular servers. It protects the server from over loading due to heavily traffic that comes in. Basically, it distrubutes the traffic evenly among the connected the servers. It periodically chech the health probe of the machines prior to sending the traffic. If the server is malfunctioning, then load balancer will divert the traffic from it and it will keep redirecting the traffic until the server doesn't work properly. 
- JumpBox limits the access of your VM to the public since, it needs private IPs of the machines cannot. In essence, it does not allow 

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the logs and system traffic.
- Filebeat watches the for change in the system structure. It acts as a logging agent which generates the log files, tail it,  forward the data for indexing
- Metricbeats collects the metrics and statistics from the operating system and from the services running on the server.

The configuration details of each machine may be found below.

| Name     | Function          | IP Address | Operating System |
|----------|-------------------|------------|------------------|
| Jump Box | Gateway           | 10.0.0.4   | Linux            |
| Web-1    | Host DWVA         | 10.0.0.5   | Linux            |                 
| Web-2    | Host DWVA         | 10.0.0.6   | Linux            |                 
| ELK      | Host DWVA         | 10.0.0.4   | Linux            |               

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jump-Box-Provisioner machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
169.57.33.126 (Public IP)

Machines within the network can only be accessed by Jump-Box-Provisioner VM.
- Which machine did you allow to access your ELK VM? Jump-Box-Provisioner
- What was its IP address? 169.57.33.126

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------|
| Jump Box | Yes/No              | 169.57.33.126        |
| Web-1    |  No                 | Local Vnet           |
| Web-2    |  No                 | Local Vnet           |
| ELK      | Yes                 | 169.57.33.126        |


### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because it allows multiple machines to configure repeatable changes at the same time which can speeds up the deployment process. Besides that, the codes keep updating when the enviorment needs to create new or update it.  

The playbook implements the following tasks:
- Download/Install Docker on the ELK server
- Download/Install/Start ELK on a docker container on hosted on the ELK server
- Download/Install/Start filebeat on the docker container running on each web server, forwarding logs to the ELK server
- Download/Install/Start metricbeat on the docker container running on each web server, forwarding metrics to the ELK server


### Target Machines & Beats
This ELK server is configured to monitor the following machines:
|   Name   |Function	IP Address |Operating System      |
|----------|---------------------|----------------------|
| Web-1    |  10.0.0.5           | Local Vnet           |
| Web-2    |  10.0.0.6           | Local Vnet           |

We have installed the following Beats on these machines:
- Filebeat
- Metricbeat

These Beats allow us to collect the following information from each machine:
- Filebeat : Monitor file changes on the system
- Metricbeat : Monitor system metriv like CPU usage, Ram etc.

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the Ansible/Elk playbook.yml to /etc/files.
- Update the /etc/ansible/hosts file to include group of machines you're trying to run the playbook.
- Run the playbook, and navigate <public_ip_of_elk_machine> :5601/app/kibana to check that the install worked as expected
