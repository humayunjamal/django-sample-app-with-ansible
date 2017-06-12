# fetch


This repo cotains the cloudformation template a.json to create the required infrastructure i.e ASG<-ELB 

it also contains the required sample django application with ansible provisioning instructions to configure/deploy the application. 


## How to Launch the application 

Step 1) Create a postgreSQL server in RDS or ec2 based. Get the endpoint and make sure the server is accessible on port 5432 by the local subnets which will be used to host the django app . Update the settings.py file with the postegreSQL endpoint in this repo. 

P.S this repo can also create/configure a local postgres db if required for testing purpose

Step 2) Use the cf template a.json to launch the application. 

The template will launch an ASG with ELB and security group configured to allow ssh port to 0.0.0./0 (you can change it in a.json to allow only your vpn ips etc) and port 80 . 

The user data of the auto scaling group is configured to download this repo and run the playbook which provision and deploys the hello app 

Tail the /var/log/cloud-init-output.log log file to check the status of a newly created instance application deployment

Step 3) Access the application via created ELB end point on port 80. 


## How to update the code 

Update the code in the repo and run fetch/ansible/ansible-playboot -i hosts deploy.yml ( make sure you update the deploy.yml hosts section to point towards the servers mentioned in your hosts file) 


## To DO  
* ASG user data ansible launch throws an error at nginx configuration copy , runs fine when its run remotely or from the box 
* make settings.py part of ansible templates so postgresql endpoint can be added in vars.yml 
* create the postgresql DB via the same cloudformation template and use the endpoint to be dynamically added to ansible playbook call command


