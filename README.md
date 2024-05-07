

![dd](https://github.com/anilyuo/ansible-playbook/assets/168365194/3dff943a-3cfc-416c-8147-19185eee975b)

# Choosing Tools to Deploy and Maintain Applications and Infrastructure

A quick reference before choosing our approach to understand mutable and immutable architecture 

https://blogs.cisco.com/developer/choosingtools01

# Basic Setup - Ansible

1. On the instance where Ansible is installed, create a new directory for your Ansible project. For example, `mkdir myproject`
2. Inside the `myproject` directory, create a new file called `hosts` (or any name you prefer for your inventory file).
3. Open the `hosts` file and add the IP addresses or DNS names of your EC2 instances, one per line. For example

```jsx
10.0.0.1
10.0.0.2
```

1. To use your PEM key for authentication, you need to configure Ansible to use the key. Create a new file called `ansible.cfg` in the `myproject` directory and add the following lines

```jsx
[defaults]
host_key_checking = False
private_key_file = /path/to/your/pem_key.pem
```

1. Replace `/path/to/your/pem_key.pem` with the actual path to your PEM key file.
2. you can run Ansible commands targeting your EC2 instances using the inventory file. For example, to ping all the instances, run:

```jsx
ansible -i hosts -m ping all

```

# Advance Setup - Dynamic Inventory

1. Install the required Python packages for the `aws_ec2` plugin:

```jsx

pip install boto3

```

1. Create a new file called `aws_ec2.yml` in the `myproject` directory and add the following content

```jsx

plugin: aws_ec2
regions: your_aws_region
```

Note: 
Replace `your_aws_region` with the AWS region where your EC2 instances are running (e.g., `us-east-1`).

1. Create a new playbook file called `sample.yml` in the `myproject` directory with the following content.

```yaml
---
- hosts: all
  tasks:
    - name: Print a message
      debug:
        msg: "Hello from {{ inventory_hostname }}!"
```

1. Run the playbook using the dynamic inventory

```yaml
ansible-playbook -i aws_ec2.yml sample.yml
```

Note:

<aside>
💡 [WARNING]: * Failed to parse /home/ubuntu/aws_ec2.yml with auto plugin: Failed to describe instances: Unable to locate credentials

</aside>

1. To resolve this issue, you need to configure AWS credentials on the instance where Ansible is running. There are several ways to do this
    
    **Environment Variables:**
    
    - Set the `AWS_ACCESS_KEY_ID` and `AWS_SECRET_ACCESS_KEY` environment variables with your AWS access key and secret key, respectively.
    
    **Instance Role:**
    
    - If your EC2 instance has an IAM role with the necessary permissions to describe EC2 instances, Ansible can use that role automatically without explicitly providing credentials.

