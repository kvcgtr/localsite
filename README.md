# localsite
Project:Local hosting automation

Tasks:
- Provide a local hosting solution for your single web page
- Create single page website from a word document 
- Automate your hosting solution

Solutions:
Install Ubuntu 20.04 - used windows subsystem for linux, Ansible to automate installation process and automation for Git, Docker to host Webserver, Jenkins CI/CD 

Requarements:
Ubuntu, Ansible, Docker, Apache HTTP Server, Git, Jenkins


1.Provide a local hosting solution for your single web page
  - Used Windows Subsystem for linux to install Ubuntu 20.04
  - Powershell terminal execute wsl --install -d Ubuntu-20.04

2.Create single page website
  - Install pandoc package to convert a word document to html
    sudo apt install pandoc
    sudo pandoc -o index.html document.docx

3.Automate your hosting solution
  - Install and configurate Ansible
    sudo apt update && sudo apt install python3 python3-pip
    sudo python3 -m pip install -U pip
    sudo python3 -m pip install paramiko
    sudo python3 -m pip install ansible
    sudo mkdir /home/$USER/{fact_cache,.ssh,inventory}
    sudo mkdir /var/log/ansible
    sudo mkdir /home/$USER/ansible/inventory/{group_vars,host_vars}
    sudo touch /home/$USER/ansible/inventory/hosts
    sudo touch /home/$USER/ansible/inventory/group_vars/all.yml
    sudo touch /home/$USER/ansible/ansible.cfg
  
  - Use ansible to execute pre created playbooks it will automatically update and install required packages
    for git preinstalled on Ubuntu
    for docker install, docker.yml
      sudo ansible-playbook project/docker.yml
    for Apache HTTP Server docke container webserver.yml
      sudo ansible-playbook project/webserver.yml
    for Jenkins, jenkins.yml
      sudo ansible-playbook project/jenkins.yml
  
  - Create a new repository on github and clone it to local (requires installation of ssh keys)
  - Upload a previously converted document to this repository
  - Run ansible playbook to upload new file to Githud
      sudo ansible-playbook project/git.yml
  
  - Open and configure Jenkins, I install the recommended plugins and add one Publish Over SSH (requires installation of ssh keys)
    Create a new job - pipeline and add 4 stages "Build", "Test", "Deploy" and "Verify Deployment" in case of changes. Everything in jenkins/config.xml
    Schedule Poll SCM to run when needed it will pull all from Github if new commits
        
  
  
