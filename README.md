# Application Deployment Playbook

This Ansible playbook automates the deployment of a Python application to target instances tagged with `Name_my_instance_dev`.

## Prerequisites

- Ansible and Python boto3 library installed on the control machine
- AWS credentials configured (IAM user/role with EC2 read permissions)
- AWS CLI installed
- SSH access to target instances
- Git repository access credentials
- Environment variables set up:
  - `GIT_SSH_KEY`: The SSH private key content for git repository access
  - `GIT_SSH_KEY_PATH`: Path where the SSH key should be stored temporarily

## Features

- Creates necessary system user and group
- Installs required system packages
- Handles Git repository cloning with secure key management
- Manages application deployment and configuration
- Includes error handling and debugging
- Performs nginx service management
- Implements proper cleanup procedures

## Variables

| Variable | Description | Default |
|----------|-------------|---------|
| git_branch | Git branch to deploy | main |
| temp_dir | Temporary directory for git clone | /tmp/my_app_clone |
| app_dir | Application installation directory | /opt/my_app |
| git_key_path | Path to store Git SSH key | From environment variable |

## Usage

1. Set up required environment variables:
```bash
export GIT_SSH_KEY='your-private-key-content'
export GIT_SSH_KEY_PATH='/path/to/store/key'
```
2. Run the playbook:
To deploy a specific branch:
```
ansible-playbook -i aws_ec2.yml deploy_my_app.yml -e "branch=feature-branch"
```