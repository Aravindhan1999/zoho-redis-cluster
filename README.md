# Zoho Redis Cluster Automation

## Overview

This project automates the provisioning and management of a six-node Redis environment using Docker and Ansible. The infrastructure is containerized using Docker Compose, and Redis installation and management are automated through Ansible playbooks and roles.

## Features

* Docker-based 6-node Ubuntu infrastructure.
* SSH-enabled containers for Ansible communication.
* Automated Redis installation using Ansible.
* Role-based Ansible project structure.
* Provision, status, upgrade, and verification operations.
* Simple CLI wrapper (`redis-tool`) for common tasks.

## Project Structure

```
zoho-redis-cluster/
├── redis-tool
├── README.md
├── ansible/
│   ├── ansible.cfg
│   ├── inventory/
│   │   └── hosts.ini
│   ├── playbooks/
│   │   ├── provision.yml
│   │   ├── status.yml
│   │   └── upgrade.yml
│   └── roles/
│       └── redis/
│           ├── defaults/
│           ├── handlers/
│           ├── tasks/
│           │   └── main.yml
│           └── templates/
├── infra/
│   ├── Containerfile
│   └── compose.yml
├── output/
│   ├── provision_output.txt
│   ├── status_output.txt
│   ├── upgrade_output.txt
│   ├── verify_output.txt
│   └── data_seed_output.txt
```

## Prerequisites

* Ubuntu / WSL2
* Docker Engine
* Docker Compose
* Ansible

## Infrastructure Setup

Build and start the six-node container environment:

```bash
cd infra
docker compose up --build -d
```

## Ansible Operations

Provision Redis on all nodes:

```bash
ansible-playbook playbooks/provision.yml
```

Check Redis status:

```bash
ansible-playbook playbooks/status.yml
```

Upgrade Redis package:

```bash
ansible-playbook playbooks/upgrade.yml
```

Verify Redis installation:

```bash
ansible redis_nodes -a "redis-server --version"
```

## redis-tool Usage

The `redis-tool` script provides a simple CLI wrapper for common operations:

```bash
./redis-tool provision
./redis-tool status
./redis-tool upgrade
./redis-tool verify
```

## Output Files

The `output/` directory contains captured execution logs generated during playbook execution:

* `provision_output.txt`
* `status_output.txt`
* `upgrade_output.txt`
* `verify_output.txt`
* `data_seed_output.txt`

## Verification

* Verified Ansible connectivity across all six nodes using:

  ```bash
  ansible redis_nodes -m ping
  ```
* Verified Redis installation across all six nodes using:

  ```bash
  ansible redis_nodes -a "redis-server --version"
  ```

## Conclusion

This project demonstrates the use of Docker and Ansible to automate the provisioning and management of a multi-node Redis environment. The solution is modular, repeatable, and easily extensible for future enhancements.
