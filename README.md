# Ansible Role Swarm

An Ansible role to automatically set up a full [Docker Swarm](https://docs.docker.com/engine/swarm/) cluster with managers and workers, shared overlay network, and automatic cleanup cronjobs.

This role is designed to work in combination with the popular [`geerlingguy.docker`](https://galaxy.ansible.com/geerlingguy/docker) role for installing Docker.

---

## 🔧 Features

-   Installs Docker Engine using `geerlingguy.docker`
-   Initializes the Swarm on the first manager node
-   Automatically joins additional manager and worker nodes
-   Creates a shared overlay network for inter-container communication
-   Sets up a shared directory for volumes or backups (`/mnt/share`)
-   Adds a weekly cronjob to prune unused Docker resources

---

## 🧱 Requirements

-   Ansible >= 2.9
-   Docker-compatible Linux OS (Debian, Ubuntu, CentOS, etc.)
-   Root or sudo privileges
-   Python packages: `docker`, `jsondiff` (installed by this role)

---

## 📦 Role Variables

```yaml
# Docker edition to install
docker_edition: "ce"

# List of required Docker-related packages
docker_packages:
    - docker-{{ docker_edition }}
    - docker-{{ docker_edition }}-cli
    - docker-{{ docker_edition }}-rootless-extras
    - docker-buildx-plugin
    - python3-jsondiff
    - python3-docker
    - containerd.io
```
