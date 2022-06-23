# AnsibleAssignment

## description
This repository includes an ansible play-book that deploys the Weight-Tracker app on 2 different enviroments(production,staging)

## installation
On the ansible controller do the following steps:

 * sudo apt update
 * sudo apt install ansible
 * sudo apt install sshpass -y
 * git clone https://github.com/OriTzadok-hub/AnsibleAssignment.git
 
On the host servers - make sure you have Python installed.

## included files
### ansible.cfg
Defined defaults in it:

 * inventory	  = hosts - assigns the hosts file to be the inventory
 * host_key_checking = False - disables ansible hosts to require ssh key (as we only use ssh via passwords)
 
### hosts
Holds all the information about the hosts - ip addresses, passwords, variables, etc

### app-deployment.yml
This is the playbook that includes all the steps to deploy our web app
it uses the following modules in this order:

- pull node-js version 14.x files
- update cache and install node js
- clone the git repository of the app
- install dotenv in the repository directory

*only for production enviroment*
- create .env file with the given variables for production env
- initate db via one of the production servers

*only for staging enviroment*
- create .env file with the given variables for staging env
- initiate the db via one of the staging servers

*back to all enviroments*
- create a cron job that deployes the app on server restart
- deploy the app

## variables
The file *hosts* contains several needed variables:
 * ip address and ssh port of each host
 * okta app info - client id/secret , okta host url
 * postgres database password, host url, and database name
 * full url of the running app - e.g http://32.42.52.62:8080
 * cookie password
 * SSH password & Become password
 
Please note that the SSH & Become passwords are set as a default to all hosts, if you have specific password for each enviroment you can just add it in the specific enviroment variables section.
 
## running the playbook
On the ansible controller write the following command(make sure you are in the repositroy directory):

*ansible-playbook app-deployment.yml*
