Verison: 1.0

Collected by: mozufferhago@gmail.com

Feel free to reach me out in case of more clarification

Django web Application Deployment strategy: 
-------------------------------------------

- First Developers should push the project code to git servers(Stash) in My case is very Simple stupid Django app 
- In case of dockerization Dockerfile should be created 
- provision the infrastructure, there are many opensource cloud automation tools for infrastructure provisioning (terraform,cloudformation,ansible)  
- Install CI/CD software like Jenkins/Bamboo 
- Link the CI/CD software with the git repo 
- Create a plan in the CI/CD software and configure the plan to build your code and apply the unit test scripts. enable automatic build to automate the compilation and the creation of the final images
- in case of dockerization our plan should  create/build docker image and tag it and then push it to the private/public docker registry
- in case of release management the docker image should be tag base on the target release number 
- use Ansible/puppet to manage the deployment to environments(Servers) --- let ansible know the release number to deploy the right docker images. if you don't care about the release management always use the latest tag  

Note: 

   I prefer the Makefile to automate the build and then let the CI/CD  execute it.  Makefile allow us to combine all the build commands at one file which is good from automation point of view. also in case of the CI/CD is not available the build can be managed from any Machine

Deployment:
----------
Make sure the following packages are installed in your box 
ansible
Boto
AWSCLI 
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

Run the following command to Provision the infrastructure and deploy django-app to AWS  

ansible-playbook -i env/inventory --private-key MozufferKey.pem  playbooks/playbooks_vpc.yml
