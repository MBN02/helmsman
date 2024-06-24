The following ansible role will create a single master and two worker nodes kuberntes cluster. 

## Prerequisites

- Ubuntu 20.04 or compatible Linux distribution
- Ansible installed (for running Ansible playbooks)
- Kubernetes knowledge

## Usage

### Setting Up a Kubernetes Cluster using anisble 

Create `anisble.cf` 

```bash
[defaults]
inventory       = /Users/mohan.kumar.bn/hosts
command_warnings=False
host_key_checking = false
forks = 20
serial = 20
callback_whitelist = timer, profile_tasks
gathering = smart
stdout_callback = yaml
color = true

[ssh_connection]
pipelining = True
```

Create a `inventory` file

```bash
[control_plane]
master-node ansible_host=192.168.X.A

[workers]
worker-node1 ansible_host=192.168.X.B
worker-node2 ansible_host=192.168.X.C

[all:vars]
ansible_python_interpreter=/usr/bin/python3

[control_plane:vars]
ansible_ssh_private_key_file= /Users/mohan.kumar.bn/.ssh/id_rsa
ansible_user= root

[workers:vars]
ansible_ssh_private_key_file= /Users/mohan.kumar.bn/.ssh/id_rsa
ansible_user= root
```

To set up a Kubernetes cluster, run the following Ansible playbook:

```yaml

setup_kubernetes.yml
---
- name: Setup Kubernetes Cluster
  hosts: all
  become: true
  roles:
    - setup-kuberntes-cluster
```

```yaml
ansible-playbook setup_kubernetes.yml
```
