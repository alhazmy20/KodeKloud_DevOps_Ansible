# Provisioning and Configuring EC2

This project serves as a practical demonstration of my learnings from the DevOps Learning Path on KodeKloud. The primary objective is to provision AWS resources and automate the configuration of EC2 instances, showcasing the utilization of the **subnet_id** of the EC2 instances.

## Project Components
- `EC2-Provision`: Ansible playbook responsible for provisioning AWS resources, including EC2 instances, Security Groups, and Key-pairs.
- `Configure-EC2`: Ansible playbook for configuring the provisioned EC2 instance.
- `inventory.ini`: A file containing a list of hosts to automate their configuration.

## Requirements
To run the playbooks in this project, ensure that the Ansible instance meets the following prerequisites:
- Ansible v2.10.17
- Python v3.6.8
- Boto3 v1.22
- Botocore v1.25.13

Additionally, you need to generate the following:
- AWS Access Keys (for provisioning AWS resources)
- SSH Keys (for SSH access to the EC2 instances and configuration)

## Usage
Follow these steps to use the project effectively:

1. **Generate AWS Access Keys:**
   - Add the keys to `variables/credentials.ansible.yaml`.

2. **Generate SSH Keys:**
   ```bash
   ssh-keygen -t rsa -b 4096 -f /path/to/your/keys
   ```
   - Add the generated SSH keys as follows:
        - Add the path to your public key `.pub` to `EC2-Provision` playbook at `with_file`.
        - Add the path to the private key `.pem` to `inventory` hosts file at `ansible_ssh_private_key_file` variable.

3. **Run the `EC2-Provision` playbook**
```bash
ansible-playbook EC2-Provision.ansible.yaml
```

4. **Add EC2 Public IP Address to `inventory` file**
    - Add the generated EC2 Public IP Address to the `inventory` hosts file at `ansible_host` variable.

5. **Run the `EC2-Configure` playbook** 
```bash
ansible-playbook -i inventory.ini EC2-Configure.ansible.yaml
```