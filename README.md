# Ansible Playbook: Ansible-security

## Description
This Ansible playbook automates the configuration of hardening SSH, installing fail2ban, and
turning on auto-update on the homelab PCs.

## Requirements

- Python3 and pip installed on your machine

## Instructions

Instructions can be found [here](https://homelab-coral.vercel.app/iac/ansible/#run-security-playbook) on how to run this playbook.

## Linting and syntax-check

You can run yamllint to lint your yaml via

```shell
yamllint .
```

You can run syntax-check to verify the playbook's imports via
```shell
ansible-playbook playbook.yml --syntax-check
```

## Configuration

- **Inventory File**: `inventory/hosts.ini`
  - Update this file to define your target hosts and group them as required.
  - Make sure to encrypt this file with ansible vault as detailed in the instructions.
- **Variables**: `vars/main.yml`
  - Customize variables in this file to configure the playbook behavior.
- **Playbook**: `playbook.yml`
  - Import tasks, handlers, and vars. This is the main file.
- **Tasks**: `tasks/*.yml`
  - `tasks.yml` is the main file that imports all the tasks from the other yml files in this directory.
  - `autoupdate.yml` contains the tasks to configure Ubuntu to auto update.
  - `fail2ban.yml` contains the tasks to install and configure fail2ban and ensure it's running.
  - `ssh.yml` contains the tasks to harden ssh.
- **Handlers**: `handlers/main.yml`
  - Handlers are special tasks that only execute when a specific condition is met. We have handlers to restart ssh, reload ufw, and reload fail2ban.

## Misc

- Fail2ban currently does not work on Ubuntu 24.04. So it's steps in ansible are disable dfor the time being, you can enable it inside `vars/vars.yml`:

```yaml
security_fail2ban_enabled: true
```

- This playbook was heavily influenced by [Jeff Gurling's playbook](https://github.com/geerlingguy/ansible-role-security)
