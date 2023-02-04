# Ansible playbook for creating a local kubernetes cluster

Following https://kubernetes.io/blog/2019/03/15/kubernetes-setup-using-ansible-and-vagrant/ and updating it where necessary for the current kubernetes version.

## Requirements

* vagrant
* libvirt
* love for k8s

## Installation

Using vagrant en libvirt we initialise 1 master en 2 worker nodes. Ansible playbooks will be copied to the machines and executed to install kubernetes and requriements and initialize the cluster. Tested on Fedora 37.

Simply execute:

`vagrant up`

Enter a node:

`vagrant ssh master`

`vagrant ssh worker-1`

`vagrant ssh worker-2`

For your convenience, find the `admin.conf` to access the cluser in the `/tmp` on your local machine. Set the context:

`export KUBECONFIG=/tmp/admin.conf`

To install Calico for networking:

`kubectl create -f calico/operator.yaml`

`kubectl apply -f calico/calicoctl.yaml`

Calico with iptables:

`kubectl apply -f calico/calico-iptables.yaml`

Calico with eBpf:

```
kubectl apply -f calico/calico-ebpf.yaml
# and to turn off kube-proxy
kubectl patch installation.operator.tigera.io default --type merge -p '{"spec":{"calicoNetwork":{"linuxDataplane":"BPF", "hostPorts":null}}}
```


To clean up everything

`vagrant destroy -f`


# Versions

The following versions will be installed:

* Ubuntu 20.04 for the nodes
* kubernetes 1.25.6
* Calico network plugin 3.25