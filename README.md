## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

[[Images/Diagram.jpg]]

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the playbook file may be used to install only certain pieces of it, such as Filebeat.

-Playbook file: /etc/ansible/install-elk.yml

This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly available, in addition to restricting overloading the network.

What aspect of security do load balancers protect? What is the advantage of a jump box?
-The load balancer is placed between your clients and servers, allowing additional security aside from your NSG. The advantage of a jump box is to have something that intercepts traffic before reaching the web servers, filters traffic, and makes it harder to hack into the servers themselves.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the data and system logs.
-What does Filebeat watch for? 
Log Data - changes and when they were made
-What does Metricbeat record? 
Metrics and statistics - sends to a specified output

The configuration details of each machine may be found below.

| Name     | Function | IP Address | Operating System |
|----------|----------|------------|------------------|
| Jump Box | Gateway  | 10.0.0.4   | Linux            |
| Web 1    | Server   | 10.0.0.7   | Linux            |
| Web 2    | Server   | 10.0.0.6   | Linux            |
| Elk VM   | Server   | 10.1.0.4   | Linux            |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jumpbox machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
-24.128.36.115 (my home external IP)

Machines within the network can only be accessed by ssh.
Which machine did you allow to access your ELK VM? What was its IP address?
-My Jump Box VM can access my Elk VM, the internal IP is 10.0.0.4

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------|
| Jump Box | Yes                 |24.128.36.115 Home IP |
| Web 1    | No                  |   10.0.0.4 Jump Box  |
| Web 2    | No                  |   10.0.0.4 Jump Box  |
| Elk VM   | No                  |   10.0.0.4 Jump Box  |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
What is the main advantage of automating configuration with Ansible?
-The advantages of Ansible playbooks are that you can edit them easily, copy and paste parts in and out to only run certain commands, and easily run commands for different servers from one playbook.

The playbook implements the following tasks:
In 3-5 bullets, explain the steps of the ELK installation play. E.g., install Docker; download image; etc._
-Install docker.io
-Install pip3
-Install docker python module
-Use more memory
-Download and launch a docker elk container
-Enable service docker on boot

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

[[Images/docker_ps_output.png]]

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
List the IP addresses of the machines you are monitoring:
-10.0.0.7 Web 1
-10.0.0.6 Web 2

We have installed the following Beats on these machines:
Specify which Beats you successfully installed:
-Filebeat
-Metricbeat

These Beats allow us to collect the following information from each machine:
In 1-2 sentences, explain what kind of data each beat collects, and provide 1 example of what you expect to see.
-Filebeat logs any changes that occur on the system and when they occurred. Example- audit logs
-Metricbeat collects metrics and statistics, outputting the info to your desired destination. Example- Apache

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the configuration file to /etc/filebeat/filebeat.yml
- Update the configuration file to include your Elk Server internal IP address.
- Run the playbook, and navigate to the Kibana web page to check that the installation worked as expected.

Answer the following questions to fill in the blanks:

Which file is the playbook? Where do you copy it?
-The playbook file is found /etc/ansible/filebeat-config.yml and is copied to /etc/filebeat/filebeat.yml

Which file do you update to make Ansible run the playbook on a specific machine? How do I specify which machine to install the ELK server on versus which to install Filebeat on?
--You would update the /etc/ansible/hosts file to add or delete specific web server or Elk Server IP addresses, you would also update the configuration file for the playbook to ensure which machine will be used.

Which URL do you navigate to in order to check that the ELK server is running?
- http://52.190.251.195:5601/app/kibana

