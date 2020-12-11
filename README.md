# CyberBootCamp
Cyber Boot Camp files
## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

CyberBootCamp/Diagrams/Wk12CloudSecurity-diagram.png

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the YAML file may be used to install only certain pieces of it, such as Filebeat.

  - install-docker.yml
  - filebeat-playbook.yml
  - install-elk.yml

This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly _____, in addition to restricting _____ to the network.  In this setup, the Load Balancer serves as the front-end public facing web page with the IP address of 168.62.10.182 for the database as well as the distributer of multiple requests made over HTTP to access the database.  These are the Web-VM's that sit behind the load balancer, all configured with the same DVWA docker image.

- What aspect of security do load balancers protect? What is the advantage of a jump box?_
  Load Balancers contribute to security for an organization becuase in the event of an attempted or succeeding DDOS attack, the load balancer will be able to offload that attack traffic from the corporate servers to a given public cloud instead, thereby protecting the web servers behind the balancer.  In addition, if the load balancer is located in the same data center as the servers, then an SSL termination which decrypts traffic before sending to the servers leaves less risk for that unencrypted traffic to be intercepted.

  A jump box is meant to serve as first and only device that admins connect to first before executing any other administrative tasks.  In this case, the Jump box in this network serves as the computer first accessed before using SSH to reach the Ansible container, from which all the other web servers or the ELK server can be remoted into via SSH.  Regarding security, it reduces multiple points of entry for breach to a single box, which has all ports and protocols blocked except for one designated.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the network and system files.
- Filebeat monitors log files, can collect log events specified by administrators and sends them to ELK statck for indexing and searching.
- Metricbeat records the metrics for the OS and services running on the server.  They are then sent to the ELK stack for review in readable format.

The configuration details of each machine may be found below.
_Note: Use the [Markdown Table Generator](http://www.tablesgenerator.com/markdown_tables) to add/remove values from the table_.

| Name         | Function    | IP Address   | Operating System |
|--------------|-------------|--------------|------------------|
| Jump Box     | Gateway     | 10.0.0.4     | Linux            |
| Web-1        |webserver    | 10.0.0.7     | Linux            |
| Web-2        |webserver    | 10.0.0.6     | Linux            |
| Web-3        |webserver    | 10.0.0.5     | Linux            |
| ELKserver    |Kibana       | 10.1.0.4     | Linux            |
| Load Balancer|Load Balancer| 168.62.10.182| DVWA            |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Load balancer machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- My public IP address: 174.52.88.247

Machines within the network can only be accessed by the Jump Box Provisioner VM.
- Which machine did you allow to access your ELK VM? What was its IP address?_
  I allowed the Jump Box to have access to the ELK VM through the Ansible container.  It's IP address is 10.0.0.4/24 in the Virtual Network
A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------|
| Jump Box | Yes                 | 174.52.88.247        |
| Web-1    |                     |                      |
| Web-2    |                     |                      |
| Web-3    |                     |                      |
|          |                     |                      |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because it allows for the ability to rapidly create another ELK machine on an as-needed basis.  It also reduces the chance to near zero that an ELK machine would have accidental incorrect configuration settings.

The playbook implements the following tasks:
- _TODO: In 3-5 bullets, explain the steps of the ELK installation play. E.g., install Docker; download image; etc._
- Install Docker IO - this will install a docker engine on ELK server to be able to run Kibana. We tell the VM to update first, then to ensure that
  if docker is not present on the machine, to make it present.
- Install python3-pip - this is a package manager for Python coding language to assist in installing python itself onto the ELK machine.
- Install Docker Module - this will allow the machine to be able to use docker to run containers using pip as the package manager for download and
  management.
- Download/Launch Docker ELK container - This part of the play is to download the actual image for the ELK stack.  The image is made by sebp and we
  want the version 7.6.1 as denoted by the 761.  We want it to be started automatically and to restart every time we turn the machine on.  We also want it to operate out of specific ports for management and for regular view access.

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

Unfortunately I was unable to successfully install ELK onto the VM the second time. There is an image of when I reached the Kibana page the first time, but then ran into problems with installing filebeat, and had decided to redo the ELK server, where i encountered problems.  There were problems with fetching the correct file from the sebp developer.  The syntax was correct and was reviewed that the playbook was written out correctly. 

If it were successful, then when I would run the docker ps command, then i would be able to see the currently running containers with their ID's followed by the name of the images used for the containers.  I would also be able to see some statistical metrics about the container creation and the respective ports it is operationg out of.

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- Again, though the machine in my Azure environment, the ELK server would have monitored the three Web VM's behind the load balancer.
  Web-1  10.0.0.7
  Web-2  10.0.0.6
  Web-3  10.0.0.5

The following beats were to be installed on these machines:
- Filebeat
- Metricbeat

These Beats allow us to collect the following information from each machine:
- Since I was not able to get the beats installed due to Azure problems or the necessary commands not working, though correct, I do not know what the captured data would look like.  I do know that filebeat looks for specified log files or events, and then forwards them through Elasticsearch or Logstash, which then can be viewed through Kibana.  Metricbeat collects specified metrics from the OS and running services on the server

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the _____ file to _____.
- Update the _____ file to include...
- Run the playbook, and navigate to the respective VM to run "curl localhost/setup.php" to check that the installation worked as expected.

- _Which file is the playbook? Where do you copy it?_
  
  I am not sure what exactly this question is asking, but I assume it means that the playbook is the install-elk.yml for the playbook to install the ELK stack and
  I dont know what the answer is supposed to be of where I copied it other than the filepath /etc/ansible/roles within the ansible container.

- _Which file do you update to make Ansible run the playbook on a specific machine? How do I specify which machine to install the ELK server on versus which to install Filebeat on?_
  
  This is configured in the hosts file within the Ansible container on the Jump Box VM.  It is found in the filepath /etc/ansible/hosts.  Within the hostsfile, there is a section with IP addresses; this is where we will put the 3 Web VM's within the group named 'webservers'.  We have also listed underneath the 'ELK' group the IP address for the ELK server.  The reason these are separate is so that we can run different playbooks for the respectively listed set of IPs.  Within each YAML script, as part of the first section listed, there is a parameter listed called 'hosts:' meaning that whichever group of IP's in the hosts file is listed here, then the YAML script would only apply to those IP's.  In the ELK script, it states that it is to be installed only on the IP's under the ELK group, and the same is for the Filebeat YAML on the webservers group.

- _Which URL do you navigate to in order to check that the ELK server is running?

I would nagvigate to ideally the private IP address of the ELK server, but at the beginning, I was able to get it to work with the public IP since it was more straightforward during the initial learning process.  Resetting the public SSH key and making a rule specific seemed to make the private IP to work.  Anyways, navigate to the public/private IP of the ELK server "http://public-privateIP:5601" to enter the management port of the Kibana page to begin importing indexed data from the filebeat installed on the 3 Webservers.  

_As a **Bonus**, provide the specific commands the user will need to run to download the playbook, update the files, etc._
