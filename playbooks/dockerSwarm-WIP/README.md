# Docker Swarm Mode setup playbook
This playbook is meant to set up a Docker Swarm mode cluster.

So far it has been tested on a three node raspberry pi cluster running Ubuntu Server 24.04 LTS.

## Folder structure

The folder structure is set up like so:

- collections
    - This is where the collections required for this to work will go, along with the requirements.yml file.

- inventory
    - The hosts.yml file is the inventory file where we define the manager and worker nodes.
    - group_vars/all.yml file to define inventory wide variables, like the ansible user name, the become method and the like.

- playbooks
    - The playbook file is here

- roles
    - The roles for the set are here.

## How to use it:

```bash
ansible-playbook playbooks/dockerSwarmDeploy.yml
```

This sets up a docker swarm node cluster. If the firewall is enabled and active, it will open the ports needed for the swarms internal communication.