# Bionic-k8s
A simple ansible buildout designed to configure a Kubernetes cluster on Ubuntu 18.04.

**Features**
- Installs docker and kubernetes dependencies
- Creates a remote admin user named 'ubuntu' on the master node
- Installs flannel network overlay on cluster
- Optional pipenv integration to use pinned version of ansible (2.10.6)

**Server Requirements**
- Three or more Ubuntu 18.04 servers
- SSH access via root or a user with passwordless sudo
- Servers should be able to communicate over a private network
  - you may have issues registering worker nodes if your master node has a default private network which is inaccessible to the worker nodes

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

- Put the IP addresses or hostnames of your servers in the ansible inventory
```
[master]
10.10.0.19

[workers]
10.10.0.20
10.10.0.21

```

- Modify the username in the .env file if you are not using root
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

NOTE: you must first run `pipenv install` or optionally run ansible-playbook without prepending `pipenv run`