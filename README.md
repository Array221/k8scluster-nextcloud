# k8scluster-nextcloud
Ansible playbook that sets up Kubernetes cluster with *ingress-nginx* and *nextcloud*.

Playbook was created for PRiR (Przetwarzanie Równoległe i Rozproszone, in english: Parallel and Distributed Processing) classes as a way to automate final project deployment.

# Requirements
Playbook requires two roles:
- **array221.clearbox** - my role, that automates basic server configuration
- **geerlingguy.docker** - role created by Jeff Geerling, that automates docker installation

Apart from that, it requires **kubernetes.core** collection to be installed.

## Installation
To install required roles for this playbook, simply run:
```shell
ansible-galaxy install -r ./roles/requirements.yml -p ./roles
```
As for **kubernetes.core** collection, run:
```shell
ansible-galaxy collection install kubernetes.core
```

# Inventory
Example **inventory.yml** file can be found in the root of this repository.

## Hosts
Your inventory should contain:
- One host named **controlPlane** that will be cluster control plane
- Group of hosts named **workers** that will join your cluster as workers

## Variables
- **user** - your username (will be created if not exists)
- **keys** - path to your SSH public keys, or URL pointing to list of keys
- **newSSHPort** - port that will be your new SSH port (set to 22, if you don't want it to be changed)
- **podNetwork** - network CIDR that will be used during cluster initialization as pod network
- **ingressExternalIP** - your external IP address, that will be passed to ingress controller
- **nextcloudDomain** - domain name that will be endpoint for nextcloud

# Executing playbook
To execute playbook, run:
```shell
./run.yml
```

If you want to pass options to **ansible-playbook** command, you can do it this way:
```shell
./run.yml <yourOptionsHere>
```

For example, if you want to get prompt for SSH and sudo passwords, you run:
```shell
./run.yml -kK
```

