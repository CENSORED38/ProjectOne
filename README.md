## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![Project One Diagram](https://user-images.githubusercontent.com/88748033/152657802-d661fd3c-5a89-4158-94c6-e9c581800498.PNG)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the Project One Elk Stack file may be used to install only certain pieces of it, such as Filebeat.

  - ![filebeat-playbook.yml] (https://github.com/CENSORED38/ProjectOne/blob/0b97e49f0edcd964230dd582eb67873d4bfdeaf7/filebeat-playbook.yml)

This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly functional, in addition to restricting traffic to the network.
- _TODO: What aspect of security do load balancers protect? What is the advantage of a jump box?_
  - A load balancer helps prevent servers crashing due to too much traffic, they also increase uptime as well as optimize productivity. 
  - A Jump-Box is a secured computer that an admin connects to before launching an administrative task or use as an origination point to connect to other servers or untrusted       environments. These admin workstations can significantly reduce the chance of a malware infection. 

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the network and system logs.
- _TODO: What does Filebeat watch for?_
  - Filebeat monitors the log files as well as the locations that you specify, then it forwards them to Elasticsearch and Logstash for indexing.
- _TODO: What does Metricbeat record?_
  - Metricbeat records metric and statistic data and transports them to the output that you specify through Elasticsearch and Logstash.

The configuration details of each machine may be found below.
_Note: Use the [Markdown Table Generator](http://www.tablesgenerator.com/markdown_tables) to add/remove values from the table_.

| Name     | Function | IP Address | Operating System |
|----------|----------|------------|------------------|
| Jump Box | Gateway  | 10.0.0.1   | Linux            |
| Web-1    | Server   | 10.0.0.9   | Linux            |
| Web-2    | Server   | 10.0.0.10  | Linux            |
| ELK      | Server   | 10.1.0.4   | Linux            |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jump-Box-Provisioner machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- 68.35.131.173

Machines within the network can only be accessed by Jump-Box-Provisioner.
- _TODO: Which machine did you allow to access your ELK VM? What was its IP address?_
  - Jump-Box-Provisioner
  - 10.0.0.6

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------|
| Jump Box | Yes                 |   68.35.131.173      |
| ELK      | No                  |   10.0.0.6           |
| Web-1    | No                  |   10.0.0.6           |
| Web-2    | No                  |   10.0.0.6           |



### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
- _TODO: What is the main advantage of automating configuration with Ansible?_ 
  -One advantage is the use of playbooks (YAML). It is a great option for management and automation. You can automate complex IT application environments by using these            playbooks

The playbook implements the following tasks:
- _TODO: In 3-5 bullets, explain the steps of the ELK installation play. E.g., install Docker; download image; etc._
- SSH into Jump-Box-Provisioner
- Start then Attach to the ansible docker
- cd into `/etc/ansibles/files` and create the elk-playbook.yml
- Run playbook by typing `ansible-playbook elk-playbook.yml` 
- ssh into ELK-SERVER to make sure that everything is up and running


The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![TODO: Update the path with the name of your screenshot of docker ps output](Images/docker_ps_output.png)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- _TODO: List the IP addresses of the machines you are monitoring_
  - 10.0.0.9 (Web-1)
  - 10.0.0.10 (Web-2)
We have installed the following Beats on these machines:
- _TODO: Specify which Beats you successfully installed_
  - Filebeat
  - Metricbeat

These Beats allow us to collect the following information from each machine:
- _TODO: In 1-2 sentences, explain what kind of data each beat collects, and provide 1 example of what you expect to see. E.g., `Winlogbeat` collects Windows logs, which we use to track user logon events, etc._
  - Filebeat is used to collect specific log files from remote machines. Some examples of Filebeat can be files are generated by       Apache, Microsoft Azure tools, the Nginx web server, and MySQL databases
  - Metricbeat collects metric data from the specified target. Some examples of what data is collected CPU Usage as well as           uptime.

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:

FILEBEAT

- Copy the filebeat-config.yml file to `/etc/ansible/files/`. 
- Update the filebeat-config.yml file to include the ELK server's private IP in lines 1106 and 1806.
- Run the playbook, and navigate to `http://<ELK-VM Public IP>/setup.php` to check that the installation worked as expected.

METRICBEAT

- Copy the metricbeat-config.yml file to `/etc/ansible/files/`.
- Update the metricbeat-config.yml file to include the ELK server's private IP in lines 62 and 96.
- Run the playbook, and navigate to `http://<ELK-VM Public IP>/setup.php` to check that the installation worked as expected.

_TODO: Answer the following questions to fill in the blanks:_
- _Which file is the playbook? Where do you copy it?_ filebeat-playbook.yml. You copy it to /etc/ansible/files
- _Which file do you update to make Ansible run the playbook on a specific machine? How do I specify which machine to install the ELK server on versus which to install Filebeat on?_ /etc/ansible/hosts file where the IP of the Virtual Machines are. You have to sepcify two seperate groups in the /etc/ansible/hosts file. One group will be the webservers which have the IPs of the virtual machines that Filebeat will be installed to. The other group is names elkservers which will have the IP of the virtual machine that ELK will be installed to. 
- _Which URL do you navigate to in order to check that the ELK server is running? http://<ELK-VM Public IP>/setup.php

_As a **Bonus**, provide the specific commands the user will need to run to download the playbook, update the files, etc._
