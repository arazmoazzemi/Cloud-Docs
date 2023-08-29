# Devstack, Latest Installation

### *Openstack installation methods:*

- All-In-One or OpenStack AIO:

- DevStack and Packstack

- Openstack-Ansible

- SaltStack OpenStack

- Puppet

- Chef

- Containerization

- Kolla / Kolla-Ansible

- TripleO / OpenStack-On-OpenStack

- OpenStack-Helm

- Fuel OpenStack (GUI- Single node - Multi-node (non-HA) -  Multi-node (HA) )

- OpenStack Autopilot

- Juju


----

:one: Guide [DevStack Installaton](https://docs.openstack.org/devstack/latest/guides/single-machine.html) 

```
sudo useradd -s /bin/bash -d /opt/stack -m stack
sudo chmod +x /opt/stack
apt-get install sudo -y || yum install -y sudo
echo "stack ALL=(ALL) NOPASSWD: ALL" | sudo tee /etc/sudoers.d/stack

```


*Note! From here on you should use the user you created. Logout and login as that user:*

```
su - stack
sudo apt-get install git -y || sudo yum install -y git
git clone https://opendev.org/openstack/devstack
cd devstack

# Make a config file:
nano local.conf

[[local|localrc]]
FLOATING_RANGE=192.168.1.224/27
FIXED_RANGE=10.11.12.0/24
ADMIN_PASSWORD=supersecret
DATABASE_PASSWORD=iheartdatabases
RABBIT_PASSWORD=flopsymopsy
SERVICE_PASSWORD=iheartksl


./stack.sh

```





