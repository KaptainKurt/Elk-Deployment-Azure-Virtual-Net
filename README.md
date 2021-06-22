# Elk-Deployment-Azure-Virtual-Net
## Automated ELK Stack Deployment


The files in this repository were used to configure the network depicted below.




![image](https://user-images.githubusercontent.com/79345125/122850563-0c3a1e80-d2d3-11eb-9db5-73e0e68bcbdd.png)


These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the yml and config file may be used to install only certain pieces of it, such as Filebeat.

[Ansible playbook.txt](https://github.com/KaptainKurt/Elk-Deployment-Azure-Virtual-Net/files/6690462/Ansible.playbook.txt)

[Hosts.txt](https://github.com/KaptainKurt/Elk-Deployment-Azure-Virtual-Net/files/6690464/Hosts.txt)

[Ansible-config.txt](https://github.com/KaptainKurt/Elk-Deployment-Azure-Virtual-Net/files/6690483/Ansible-config.txt)

[Elk-config.txt](https://github.com/KaptainKurt/Elk-Deployment-Azure-Virtual-Net/files/6690467/Elk-config.txt)

[filebeat-playbook.txt](https://github.com/KaptainKurt/Elk-Deployment-Azure-Virtual-Net/files/6690468/filebeat-playbook.txt)

[Filebeat-config.txt](https://github.com/KaptainKurt/Elk-Deployment-Azure-Virtual-Net/files/6690470/Filebeat-config.txt)

[metricbeat-playbook.txt](https://github.com/KaptainKurt/Elk-Deployment-Azure-Virtual-Net/files/6690471/metricbeat-playbook.txt)

[metricbeat-config.txt](https://github.com/KaptainKurt/Elk-Deployment-Azure-Virtual-Net/files/6690472/metricbeat-config.txt)

This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build




### Description of the Topology


The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.


Load balancing ensures that the application will be highly redundant, in addition to restricting stress to the network.
What aspect of security do load balancers protect? 
* Web Traffic, Web Security, Availability
What is the advantage of a jump box?
* Access Control, Automation, Security, Network segmentation
Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the data and system logs.
 What does Filebeat watch for? 
* Gathers log events, and sends them to Elasticsearch or logstashing for indexing. These log files are grabbed from the location the user specifies.
 What does Metricbeat record?
* Gathers the metrics and statistics that it collects and sends them to the output that the user specifies, such as Elasticsearch or Logstash.


The configuration details of each machine may be found below.
_Note: Use the [Markdown Table Generator](http://www.tablesgenerator.com/markdown_tables) to add/remove values from the table_.


| Name          | Function      | IP Address                | OS    |
|---------------|---------------|---------------------------|-------|
| Jump Box      | Gateway       | 10.0.0.4                  | Linux |
| Web1          | Web Server    | 10.0.0.5                  | Linux |
| Web2          | Web Server    | 10.0.0.6                  | Linux |
| Web3          | Web Server    | 10.0.0.7                  | Linux |
| Elk Server    | Elk Server    | 10.2.0.10 / 13.89.232.107 | Linux |
| Load balancer | Load Balancer | Static External IP        | Linux |


### Access Policies


The machines on the internal network are not exposed to the public Internet. 


Only the Elk Server machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
Workstation Public IP through tcp 5601


Machines within the network can only be accessed by Workstation and Jump-Box-Provisioner.
Jump-Box-Provisioner IP: 10.0.04 via SSH
Workstation Public IP via port TCP 5601


A summary of the access policies in place can be found in the table below.


| Name          | Publicly Accessible | Allowed IP Addresses             |
|---------------|---------------------|----------------------------------|
| Jump Box      | No                  | Workstation Public IP on SSH 22  |
| Web1          | No                  | 10.0.0.4 on SSH 22               |
| Web2          | No                  | 10.0.0.4 on SSH 22               |
| Web3          | No                  | 10.0.0.4 on SSH 22               |
| Elk Server    | No                  | Workstation & SSH                |
| Load balancer | No                  | Workstation Public IP on HTTP 80 |


### Elk Configuration


Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because Ansible lets you quickly and easily deploy multi tier apps. You won't need to write custom code to automate your systems; you list the tasks required to be done by writing a playbook, and Ansible will figure out how to get your systems to the state you want them to be in.
The playbook implements the following tasks:
Specify a different group of machines as well as a different remote user


  ![image](https://user-images.githubusercontent.com/79345125/122850512-f4fb3100-d2d2-11eb-8fe3-b01b3b075969.png)






Increase System Memory


  
![image](https://user-images.githubusercontent.com/79345125/122850494-ec0a5f80-d2d2-11eb-8e03-1c4727706c6c.png)





Install the following services

![image](https://user-images.githubusercontent.com/79345125/122850441-d5fc9f00-d2d2-11eb-8ce1-a15be228f973.png)

  

Expose  these published ports
  
![image](https://user-images.githubusercontent.com/79345125/122850477-e01e9d80-d2d2-11eb-8af4-e46029c32b7f.png)



The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.


 ![Docker ps screenshot](https://user-images.githubusercontent.com/79345125/122850674-460b2500-d2d3-11eb-88fe-4b386f98f56c.png)
 



### Target Machines & Beats
This ELK server is configured to monitor the following machines:
* Web1: 10.0.0.5
* Web2 10.0.0.6
* Web3 10.0.0.7


We have installed the following Beats on these machines:


*Filebeat and MetricBeat
*Elk Server, Web1, Web2 and Web3


These Beats allow us to collect the following information from each machine:


Metricbeat: System statistics and metrics
Filebeat: Log events


### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 


SSH into the control node and follow the steps below:


For ELK VM Configuration:
Copy the Ansible ELK Installation and VM Configuration
Run the playbook using this command : ansible-playbook install-elk.yml


For Filebeat:
- Copy the /etc/ansible/files/filebeat-config.yml file to /etc/filebeat/filebeat-playbook.yml
- Update the  filebeat-playbook.yml file to include.
curl -L -O https://artifacts.elastic.co/downloads/beats/filebeat/filebeat-7.6.1-amd64.deb
curl -L -O https://artifacts.elastic.co/downloads/beats/filebeat/filebeat-7.6.1-amd64.deb
Update the filebeat-config.yml file root@54c0a059c0b0:/etc/ansible/files# nano filebeat-config.yml


Run the playbook using this command ansible-playbook filebeat-playbook.yml and navigate to Kibana > Logs : Add log data > System logs > 5:Module Status > Check data to check that the installation worked as expected.


For METRICBEAT:


Download Metricbeat playbook using this command:
curl -L -O https://gist.githubusercontent.com/slape/58541585cc1886d2e26cd8be557ce04c/raw/0ce2c7e744c54513616966affb5e9d96f5e12f73/metricbeat > /etc/ansible/files/metricbeat-config.yml
Copy the /etc/ansible/files/metricbeat file to /etc/metricbeat/metricbeat-playbook.yml
Update the filebeat-playbook.yml file to include installer
curl -L -O https://artifacts.elastic.co/downloads/beats/metricbeat/metricbeat-7.6.1-amd64.deb
Update the metricbeat file rename to metricbeat-config.yml
root@54c0a059c0b0:/etc/ansible/files# nano metricbeat-config.yml




