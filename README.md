# ansible-playbook
#1. Installing Ansible on Ansible-Master
  ## Update the package index
sudo apt update

## Install the required dependencies
sudo apt install software-properties-common

## Add the Ansible repository
sudo apt-add-repository --yes --update ppa:ansible/ansible

## Install Ansible
sudo apt install ansible
2. Ansible Configuration
  sudo vim /etc/ansible/hosts
  [servers]
server1 ansible_host=18.206.189.126
server2 ansible_host=3.81.158.72
server3 ansible_host=54.162.81.197

[servers:vars]
ansible_python_interpreter=/usr/bin/python3
ansible_user=ubuntu
ansible_ssh_private_key_file=/home/ubuntu/.ssh/ansible-key.pem

3. Connectivity Testing with Ansible Ping
  ansible servers -m ping -k
4. Develop palybook 

![dd](https://github.com/anilyuo/ansible-playbook/assets/168365194/3dff943a-3cfc-416c-8147-19185eee975b)



