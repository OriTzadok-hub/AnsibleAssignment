# AnsibleAssignment

## description
This repository includes an ansible play-book that deploys the Weight-Tracker app published artifact on 2 different enviroments(production,staging) - during a release pipeline.

The staging enviroment deployment is automatic (continuous deployment) and the production enviroment deployment needs to be triggered manually (continuous delivery)

## installation
On the ansible controller do the following steps:

 * sudo apt update
 * sudo apt install ansible
 * sudo apt install sshpass -y
 * git clone https://github.com/OriTzadok-hub/AnsibleAssignment.git
 
On the host servers - make sure you have Python installed.

## included files

### hosts
each stage in the release pipeline (staging stage and production stage) needs to have an inventory file that holds the hosts data and the .env file data of the current stage.(it is not added to git due to security reasons)

### app-deployment.yml
This is the playbook that includes all the steps to deploy our web app
it uses the following modules in this order:


- install zip
- unarchive the artifact in the hosts
- pull node-js version 14.x files
- update cache and install node js
- install dotenv in the unarchived artifact directory

- create .env file with the given variables for production env
- initate db via one of the production servers

- create a cron job that deployes the app on server restart
- deploy the app

## variables
The inventory files contains several needed variables:
 * ip address and ssh port of each host
 * okta app info - client id/secret , okta host url
 * postgres database password, host url, and database name
 * full url of the running app - e.g http://32.42.52.62:8080
 * cookie password
 * SSH password & Become password
