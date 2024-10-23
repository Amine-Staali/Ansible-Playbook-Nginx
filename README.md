# Ansible Playbook: Deploy Nginx Web App

## Overview

This Ansible playbook is designed to automate the deployment of an Nginx web application on a virtual machine (VM). It installs Nginx, configures a simple HTML page, and ensures that HTTP traffic is allowed through the firewall.

## Requirements

- Ansible installed on your control machine.
- Access to a VM with Ubuntu or a similar distribution.
- The target VM is listed in the `hosts.ini` file under the group `web_servers`.
- SSH access to the target VM using key-based authentication.

## Playbook Breakdown

### Playbook Name
- **Deploy Nginx web app on VM**

### Hosts
- **web_servers**: The group of hosts where the playbook will be executed.

### Become
- **yes**: The playbook will run with elevated privileges (sudo).

### Tasks

1. **Install Nginx**
   - Uses the `apt` module to install the Nginx package if it is not already present.
   - Updates the package cache.

2. **Start Nginx Service**
   - Uses the `service` module to ensure the Nginx service is started and enabled to start on boot.

3. **Deploy a Simple HTML Page**
   - Uses the `copy` module to create a simple HTML file at `/var/www/html/index.html`.
   - The HTML content includes a welcome message for the web app.
   - The file is owned by `www-data` and has appropriate permissions set to `0644`.

4. **Ensure Firewall Allows HTTP Traffic**
   - Uses the `ufw` module to allow traffic on the 'Nginx Full' profile, enabling HTTP and HTTPS traffic.

## Usage

1. Clone the repository or copy this playbook to your Ansible control machine.
2. Update hosts.ini file to include your target VM under the `web_servers` group.
3. Run the playbook with the following command:

   ```bash
   ansible-playbook -i hosts.ini deploy_nginx.yml --ask-become-pass
