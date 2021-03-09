# Bionic-k8s
A simple ansible buildout designed to configure a Kubernetes cluster on Ubuntu 18.04.

**Features**
- Installs docker and kubernetes
- Creates a remote non-root user named 'ubuntu' with passwordless sudo
on all nodes
- Installs the flannel network overlay v0.13.0
- Optional `pipenv` integration

**Server Requirements**
- Three or more Ubuntu 18.04 servers with at least 2vCPU's and 2GB of
RAM each
- SSH access via root or a user with passwordless sudo
- Servers should be able to communicate over a private network
  - Issues may arise while registering worker nodes if the master node has a default private network which is inaccessible to the worker nodes

**Local requirements**
- Python 3.8 and pipenv installed

OR
- Ansible installed (tested with 2.10.6)

**Usage**
- Copy the default .env and hosts files:
```
# cp .env-sample .env
# cp hosts-sample hosts
```

- Put the IP addresses or hostnames of the servers in the ansible inventory
```
[master]
10.10.0.19

[workers]
10.10.0.20
10.10.0.21

```

- Modify the username in the .env file (if not using `root`)
```
ANSIBLE_REMOTE_USER=someuser
```
- Run `main.yml` to configure the master and worker nodes
```
# pipenv run ansible-playbook main.yml
```

- Run `register-workers.yml` to join workers to the cluster
```
# pipenv run ansible-playbook register-workers.yml
```

NOTE: Run `pipenv install` first, or optionally run ansible-playbook without prepending `pipenv run`.
