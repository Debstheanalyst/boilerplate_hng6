# Automated Deployment and Configuration with Ansible for Golang Boilerplate

## Overview

This project uses Ansible to automate the deployment and configuration of a Golang boilerplate application on a Linux server. The setup includes PostgreSQL database configuration, application deployment, Nginx reverse proxy setup, and logging.

## Requirements

- Ansible
- Ubuntu 22.04 server
- SSH access to the server
- Golang, PostgreSQL, and Nginx installed on the server

## Setup Instructions

### 1. Clone the Repository

Clone the repository to your local machine:

```bash
git clone https://github.com/hngprojects/hng_boilerplate_golang_web.git
cd hng_boilerplate_golang_web
```

### 2. Create Inventory File

Create an `inventory.cfg` file with your server details:

```ini
[hng]
your_server_ip_or_dns ansible_user=ubuntu ansible_ssh_private_key_file=path_to_your_private_key
```

### 3. Update Variables

Edit the `main.yaml` file to set your PostgreSQL credentials and other variables:

```yaml
vars:
  postgres_user: admin
  postgres_password: secure_password
  db_name: myappdb
  app_directory: /opt/stage_5b
  log_directory: /var/log/stage_5b
```

### 4. Run the Playbook

Execute the Ansible playbook:

```bash
ansible-playbook -i inventory.cfg main.yaml -b
```

## Playbook Structure

### Tasks

- **Common Tasks**: Create user, update apt cache, install required packages, ensure necessary directories exist, clone the repository.
- **PostgreSQL Tasks**: Install PostgreSQL, start service, save credentials, create database and user.
- **Application Tasks**: Configure Git, change ownership of the application directory, install Go, build the application, configure environment variables, create systemd service, start the application.
- **Nginx Tasks**: Install Nginx, start service, configure reverse proxy, test and reload configuration.

## Logging

Logs are saved in `/var/log/stage_5b`:
- `error.log`: Standard error logs
- `out.log`: Standard output logs

Both log files are owned by the `hng` user.

## Notes

- Ensure the `path_to_your_private_key` in `inventory.cfg` points to your SSH private key file.
- Make sure the server is accessible via SSH and Ansible can connect to it.

## Troubleshooting

If there are any issues during the playbook execution, refer to the Ansible documentation and check the log files for detailed error messages.

---
