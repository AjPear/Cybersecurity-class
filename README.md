# Cybersecurity-class
projects from cybersecurity class
## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

(https://user-images.githubusercontent.com/90866513/150437674-c3d20889-0f28-4472-9fe5-72122b25cadd.png)


These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the ansible file may be used to install only certain pieces of it, such as Filebeat.

  - /etc/ansible/install-elk-playbook.yml

This document contains the following details:
- Description of the Topologu
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly efficient, in addition to restricting traffic to the network.
-  What aspect of security do load balancers protect? load balancers ensure availability and can help mitgate the effects of a DDOS attack. What is the advantage of a jump box?_A jump box allows access from a single point that can be mointored and secured.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the logs and system files.
-  What does Filebeat watch for?_Filebeat watches for information on the system that has changed and watches and logs file locations and sends logs of events.
-  What does Metricbeat record?_Metricbeat uses the statistics and metrics of the system and displays them in readable format.

The configuration details of each machine may be found below.
_Note: Use the [Markdown Table Generator](http://www.tablesgenerator.com/markdown_tables) to add/remove values from the table_.

| Name      | Function  | IP Address | Operating System   |
|-----------|-----------|------------|--------------------|
| Jump Box  | Gateway   | 10.0.0.4   | Linux Ubuntu 20.04 |
| Web-1     | Server    | 10.0.0.7   | Linux Ubuntu 20.04 |
| Web-2     | Server    | 10.0.0.8   | Linux Ubuntu 20.04 |
| ELK-Server| Elk Server| 10.1.0.4   | Linux Ubuntu 20.04 |

### Access Policies

The machines on the internal network are not exposed to the public Internet.

Only the JumpBox machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- 97.83.81.181

Machines within the network can only be accessed by SSH.
-  Which machine did you allow to access your ELK VM? Jumpbox VM What was its IP address?_Private IP of 10.0.0.4

A summary of the access policies in place can be found in the table below.

| Name       | Publicly Accessible | Allowed IP Addresses |
|------------|---------------------|----------------------|
| Jump Box   | Yes                 | 97.83.81.181         |
| Web-1      | No                  | 10.0.0.4             |
| Web-2      | No                  | 10.0.0.4             |
| Elk-Server | No                  | 10.0.0.4             |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
-  What is the main advantage of automating configuration with Ansible?_Ansible allows for the task to be automated and run the exact same way everytime this saves time and ensures the configuration is the same.

The playbook implements the following tasks:
- -name : install docker.io apt: Update_cache: yes force_apt_get: yes name: docker.io state: present
- -name : Install python3-pip apt: force_apt_get: yes name: python3-pip state : present
- -name : Install Docker module pip: name: docker state: present

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

!(Images/ELk_server_screenshot_1.jpg)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- Web-1 10.0.0.7 and Web-2 10.0.0.9

We have installed the following Beats on these machines:
- Filebeats and Metricbeats

These Beats allow us to collect the following information from each machine:
- File beats collects logs and allows us to see system changes like when sudo commands are used. Metricbeats monitors the metrics of the system and can show increase RAM usage.

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned:

SSH into the control node and follow the steps below:
- Copy the playbook file to /etc/ansible/files.
- Update the configuration file to include the ELK server VM and Webserver VMs listing their private IP addresses
- Run the playbook, and navigate to ELK VM to check that the installation worked as expected.

 Answer the following questions to fill in the blanks:_
- Which file is the playbook?/etc/ansible/file/filebeat-configuration.yml  Where do you copy it? to the files folder
- Which file do you update to make Ansible run the playbook on a specific machine? The Hosts file. How do I specify which machine to install the ELK server on versus which to install Filebeat on? change the
- Which URL do you navigate to in order to check that the ELK server is running? http://(ELK Server External IP):5601/app/kibana


Network Security Domain:
Question 1: Faulty Firewall
Suppose you have a firewall that's supposed to block SSH connections, but instead lets them through. How would you debug it?

If a firewall is not blocking SSH connections like it should be then the best way to debug it would be to first start by checking the firewall setting on port 22 which allows the SSH connections. If port 22 is not blocked then SSH connections can be made, or if certain IP addresses are allowed to use port 22 it will enable those addresses to use SSH. When setting up the virtual network for project one we started by creating firewall rules. This allowed us to eliminate traffic from all other sources. Port 22 traffic was limited to the IP address on the user computer. This allowed the user to SSH into the virtual network. If this rule were changed to block all incoming traffic to port 22 it would effectively stop all SSH traffic. The advantage of this would be no incoming SSH traffic, but the disadvantage would be if network administrators need to SSH in for any reasons that would be blocked as well.

Question 2: Unsecured Web Server
Suppose you find a server running HTTP on port 80, despite compliance guidelines requiring encryption in motion. What do you do?

If I found a server running HTTP on port 80 which does not follow the guidelines of encryption in motion, I would check the server settings. In project one for my class, we ran servers on port 80 for testing, which is why they were on port 80. For a real deployment you would want to block traffic from port 80 and instead use port 443 which is HTTPS which is the compliance following standard. This could be changed by altering the firewall rules and denying port 80 traffic instead allowing port 443 traffic. This would harden the network and ensure compliance with guidelines. The client traffic will be blocked to port 80 and can be redirected to port 443 which will allow incoming traffic. This solution should be able to be set up in the firewall rules and left to run. 
