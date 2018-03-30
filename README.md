# Best Songs (Static)

Project to demonstrate using Ansible to:
* Setup and configure Debian based Web Server, Application Server and DB server
* Deploy sample web application queries the database and displays a random song from [list of 100 songs](http://www.johnsandford.org/prey16x1.html).
* Leveraged Ansible Tutorial by @nbkr
* [Best Songs (Dynamic)](https://github.com/skipluck/bestsongs-dynamic) that uses Dynamic inventory for AWS

Web Server | App Server | DB server
-----------|------------|----------
Install common software packages | Install common software packages | Install common software packages
Configure SSH banner | Configure SSH banner | Configure SSH banner
Install Apache | Install gunicorn (Python HTTP server) | Install MySQL
Configure Apache as reverse proxy | Configure gunicorn to run as service using supervisor | Create database
Restart Apache | Deploy application code | Create table and import sample data
| Restart services |

## Prerequisites
* 3 target servers that have been configured for [public key SSH authentication](https://www.ssh.com/ssh/public-key-authentication)

## Running this project
Open terminal window and run the following commands

### Install Ansible on Ubuntu Linux
````
sudo apt-get update
sudo apt-get install git python3 python3-pip
pip3 install --upgrade pip
pip3 install virtualenv
````

### Cloning this project from github
````
git clone https://github.com/skipluck/bestsongs-static
````

### Creating Ansible Project Virtual Environment
````
cd bestsongs-static
virtualenv --python=/usr/bin/python3 BestSongs
source BestSongs/bin/activate
````

### Installing Ansible and other packages
````
pip3 install ansible
````

### Edit hosts files
Open hosts file in your favorite editor and add respective hostsnames for web, app and db servers

#### Sample hosts files
````
[webservers]
ec2-54-210-56-37.compute-1.amazonaws.com ansible_user=ubuntu
[appservers]
ec2-34-229-178-128.compute-1.amazonaws.com ansible_user=ubuntu
[dbservers]
ec2-35-172-201-189.compute-1.amazonaws.com ansible_user=ubuntu
````

### Executing Ansible playbook
````
ansible-playbook -i hosts playbook.yml
````

### Exiting Virtual Environment
````
deactivate
````
