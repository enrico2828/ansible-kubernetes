# Ansible playbook for creating a local kubernetes cluster

Following https://kubernetes.io/blog/2019/03/15/kubernetes-setup-using-ansible-and-vagrant/ and updating it where necessary for the current kubernetes version.

## Requirements

* vagrant
* virtualbox
* love for k8s

## Installation

Using vagrant en virtualbox we initialise 1 master en 2 worker nodes. Ansible playbooks will be copied to the machines and executed to install kubernetes and requriements and initialize the cluster.

Simply execute:

`vagrant up`

Enter a node:

`vagrant ssh master`

`vagrant ssh worker-1`

`vagrant ssh worker-2`

For your convenience, find the `admin.conf` to access the cluser in the `kubernetes-setup` folder of this project.

To clean up everything

`vagrant destroy -f`


# Versions

The following versions will be installed:

* Ubuntu 18.04 for the nodes
* kubernetes 1.19.0
* Calico network plugin 3.14