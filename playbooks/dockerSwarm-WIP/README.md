# Docker Swarm Mode setup playbook
This playbook is meant to set up a Docker Swarm mode cluster.
If the firewall is enabled and active, it will open the ports needed for the swarms internal communication.

So far it has been tested on a three node raspberry pi cluster running Ubuntu Server 24.04 LTS.

## Folder structure

The folder structure is set up like so:

- collections/
    - This is where the collections required for this to work will go, along with the requirements.yml file.

- inventory/
    - The hosts.yml file is the inventory file where we define the manager and worker nodes.
    - group_vars/all.yml file to define inventory wide variables, like the ansible user name, the become method and the like.

- playbooks/
    - The playbook file is here

- roles/
    - The roles for the set are here.

- ansible.cfg
    - project specific ansible.cfg file. Here we can define the location of the private key file, used for ansible to login to the targets.

## Prerequisites
This project depends on a few things to work.

- ansible or ansible-core.
    - This project have been created and tested with ansible-core.

- ansible user account on the targets
    - In this case, it is called ansibleuser, but it could be called whatever. It could also be the root account, if you want. Whatever account name is used, should be defined in the ansible.cfg file.
    - a public key should have been copied over to the targets with the `ssh-copy-id` command, to the ansible user account on the target. If we want to use password authentication instead, the `ansible-playbook` command should be appended with `-k`.

- These ansible-galaxy collections.
    - install the collections with the command: `ansible-galaxy collection install -r collections/requirements.yml`
    - They are listed in the collections/requirements.yml file.:
        - ansible.utils
        - community.general
        - ansible.posix
        - community.docker

## How to use it

```bash
ansible-playbook playbooks/dockerSwarmDeploy.yml
```

<<<<<<< Updated upstream
=======
This sets up a docker swarm node cluster. If the firewall is enabled and active, it will open the ports needed for the swarms internal communication.

## To do
  - Test on a different architecture than arm.
  - Create roles for setting up a swarm on RHEL
>>>>>>> Stashed changes
