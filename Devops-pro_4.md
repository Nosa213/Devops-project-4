# ANSIBLE CONFIGURATION MANAGEMENT 
Ansible Client as a Jump Server (Bastion Host)
A Jump Server (sometimes also referred as Bastion Host) is an intermediary server through which access to internal network can be
provided. If you think about the current architecture you are working on, ideally, the webservers would be inside a secured network 
which cannot be reached directly from the Internet. That means, even DevOps engineers cannot SSH into the Web servers directly and 
can only access it through a Jump Server – it provide better security and reduces attack surface.

On the diagram below the Virtual Private Network (VPC) is divided into two subnets – Public subnet has public IP addresses and Private
subnet is only reachable by private IP addresses.


![6033](https://user-images.githubusercontent.com/85270361/210153615-ea6cf398-05d3-45d0-9ea4-6daffac7fa4c.PNG)


When you reach Project 15, you will see a Bastion host in proper action. But for now, we will develop Ansible scripts to simulate 
the use of a Jump box/Bastion host to access our Web Servers.

## Task
1. Install and configure Ansible client to act as a Jump Server/Bastion Host
2. Create a simple Ansible playbook to automate servers configuration


## Step 1 - INSTALL AND CONFIGURE ANSIBLE ON EC2 INSTANCE
<p>Update Name tag on your Jenkins EC2 Instance to Jenkins-Ansible. We will use this server to run playbooks.</p>

![image](https://github.com/Nosa213/Devops-project-4/assets/125190958/f84fba6c-0f34-4d53-8e74-0cebbcc8af92)


<p>In your GitHub account create a new repository and name it ansible-config-mgt.</p>


<p>Instal Ansible</p>

    sudo apt update
    sudo apt install ansible
    
<p>Check your Ansible version by running:</p>
	
    ansible --version
    
![image](https://github.com/Nosa213/Devops-project-4/assets/125190958/4974061f-0a2a-4ae1-872c-ee8a42bcbb75)

<p>Configure Jenkins build job to save your repository content every time you change it:</p>

<p>Create a new Freestyle project ansible in Jenkins and point it to your ‘ansible-config-mgt’ repository.</p>


![image](https://github.com/Nosa213/Devops-project-4/assets/125190958/ee8cdd9a-0d74-4a61-a8c3-ba9ae1686e9e)

<p>Configure Webhook in GitHub and set webhook to trigger ansible build.</p>

![image](https://github.com/Nosa213/Devops-project-4/assets/125190958/98444fcd-9069-4967-be03-41d3372addfd)

<p>Configure a Post-build job to save all (**) files, like you did it in Project 9.</p>

## Post-build Actions

![image](https://github.com/Nosa213/Devops-project-4/assets/125190958/542bc4d1-f294-4384-b64e-384e887c1e5d)

Test your setup by making some change in README.MD file in master branch and make sure that builds starts automatically and Jenkins saves the files

![image](https://github.com/Nosa213/Devops-project-4/assets/125190958/2f1e2fec-d03b-4a3b-8384-106c9be27938)

![image](https://github.com/Nosa213/Devops-project-4/assets/125190958/9ff4d81a-cbbf-4df7-afe3-5ac58009f040)


Confirm if Jenkins saves the files (build artifacts) in following folder:

```
ls /var/lib/jenkins/jobs/ansible/builds/<build_number>/archive/
```
