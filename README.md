# Automated build of k3s Cluster with MetalLB

This playbook will build a Kubernetes cluster with `k3s` and MetalLB via `ansible`.

## 📖 k3s Ansible Playbook

Build a Kubernetes cluster using Ansible with k3s. The goal is easily install a HA Kubernetes cluster on machines running:

- [X] Debian
- [X] Ubuntu
- [X] CentOS

on processor architecture:

- [X] x64
- [X] arm64
- [X] armhf

## ✅ System requirements

* Deployment environment must have Ansible 2.4.0+.
* `server` and `agent` nodes should have passwordless SSH access, if not you can supply arguments to provide credentials `-ask-pass --ask-become-pass` to each command.

### 🍴 Preparation

First create a new directory based on the `sample` directory within the `inventory` directory:

```bash
cp -R inventory/sample inventory/my-cluster
```

Second, edit `inventory/my-cluster/hosts.ini` to match the system information gathered above. 

For example:

```ini
[master]
192.168.30.38
192.168.30.40

[node]
192.168.30.41
192.168.30.42

[k3s_cluster:children]
master
node
```

If needed, you can also edit `inventory/my-cluster/group_vars/all.yml` to match your environment.

### ☸️ Create Cluster

Start provisioning of the cluster using the following command:

```bash
ansible-playbook site.yml -i inventory/my-cluster/hosts.ini
```

### 🔥 Remove k3s cluster

```bash
ansible-playbook reset.yml -i inventory/my-cluster/hosts.ini
```

## ⚙️ Kube Config

To copy your `kube config` locally so that you can access your **Kubernetes** cluster run:

```bash
scp debian@master_ip:~/.kube/config ~/.kube/config
```

----

Thanks to these repos for code and ideas:

* [k3s-io/k3s-ansible](https://github.com/k3s-io/k3s-ansible)
* [technotim/k3s-ansible](https://github.com/geerlingguy/turing-pi-cluster)
