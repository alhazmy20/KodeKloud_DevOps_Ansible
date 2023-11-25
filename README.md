
# Provisioning and Configuring EC2 

This is a simple project created to showcase what I've learned while attending the DevOps Learning Path on KodeKloud.
- The purpose of this project is to Provision AWS Resources and Automate EC2 configuration to show the **subnet_id** of the EC2 instances. 

## Contains
- `EC2-Provision` Ansible playbook to provision AWS resources (EC2 instance, Security Group, Key-pairs).
- `Configure-EC2` Ansible playbook to configure provisioned EC2 instance/
- `inventory.ini` A file that contains a list of hosts to automate its configuration.

## Requirements 
- To run the playbooks in this project you are required to install the following on the Ansible instance: 
    - Ansible v2.10.17
    - python v3.6.8
    - boto3 v1.22
    - botocore v1.25.13
- Generate AWS Access Keys (to provision AWS resources)
- Generate SSH Keys (to SSH into EC2 instance and configure it)

## Usage
- Generate AWS Access Keys then add the keys to `variables/credentials.ansible.yaml`
- Generate SSH Keys using the following command:
```bash
ssh-keygen -t rsa -b 4096 -f /path/to/your/keys
```
   - Add the generated SSH keys as follows:
        -  Add the path to your public key `.pub` to `EC2-Provision` playbook at `with_file`.
        - Add the path to the private key `.pem` to `inventory` hosts file at `ansible_ssh_private_key_file` variable.

- Run the `EC2-Provision` playbook to provision AWS resources using:
```bash
ansible-playbook EC2-Provision.ansible.yaml
```
- Add the generated EC2 Public IP Address to the `inventory` hosts file at `ansible_host` variable.
- Run the `EC2-Configure` playbook with the `inventory` hosts file to configure the EC2 instances using:
```bash
ansible-playbook -i inventory.ini EC2-Configure.ansible.yaml
```