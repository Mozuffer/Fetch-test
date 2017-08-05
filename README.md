Verison: 1.0

Collected by: mozufferhago@gmail.com

Feel free to reach me out in case of more clarification

Django web Application Deployment strategy: 
-------------------------------------------

1- First Developers should push the project code to git servers(Stash) in My case is very Simple stupid Django app 
2- In case of dockerization Dockerfile should be created 
3- provision the infrastructure, there are many opensource cloud automation tools for infrastructure provisioning (terraform,cloudformation,ansible)  
3- Install CI/CD software like Jenkins/Bamboo 
4- Link the CI/CD software with the git repo 
5- Create a plan in the CI/CD software and configure the plan to build your code and apply the unit test scripts. enable automatic build to automate the compilation and the creation of the final images
6- in case of dockerization our plan should  create/build docker image and tag it and then push it to the private/public docker registry
7- in case of release management the docker image should be tag base on the target release number 
8- use Ansible/puppet to manage the deployment to environments(Servers) --- let ansible know the release number to deploy the right docker images. if you don't care about the release management always use the latest tag  

Note: 

   I prefer the Makefile to automate the build and then let the CI/CD  execute it.  Makefile allow us to combine all the build commands at one file which is good from automation point of view. also in case of the CI/CD is not available the build can be managed from any Machine


Ansible:
--------
Ansible is an open-source automation engine that automates software provisioning, configuration management, and application deployment
for more details about ansible, ansible playbook and roles please visit http://docs.ansible.com/

Playbook:  contain all the ansible playbooks
  vpc.yml: vpc playbook  
roles: contains ansible roles 
docker: contains simple djgango dockerise app
env: contain inventory file
ansible.cfg: ansible main configuration file 

Deployment instructions:
Create django Docker Image:
Enter this directory "docker/django_app" and run make the instruction is below
cd  docker/django_app
make 
The above instruction build django docker image "mozuffer/djangoapp" and pusched to the docker registry

Provision the infrastructure and deploy django-app to AWS 

ansible-playbook -i inventory -u ec2-user -k -K  playbook/vpc.yml

