# Install opennebula fronend kvm ubuntu22.04.2

***Install easy way***

***01-Get Frontend Only ---> run on frontend node***


```
sudo apt-get update -y
sudo apt-get upgrade -y
wget 'https://github.com/OpenNebula/minione/releases/latest/download/minione'
sudo bash minione --frontend
```

***02-Get opennebula-node-kvm Only for edge nodes ---> run on compute node***
```
sudo apt-get update -y
sudo apt-get upgrade -y
sudo apt-get -y install gnupg wget apt-transport-https
wget -q -O- https://downloads.opennebula.io/repo/repo2.key | apt-key add -
wget -q -O- https://downloads.opennebula.io/repo/repo2.key | gpg --dearmor --yes --output /etc/apt/trusted.gpg.d/opennebula.gpg
sudo echo "deb https://downloads.opennebula.io/repo/6.6/Ubuntu/22.04 stable opennebula" > /etc/apt/sources.list.d/opennebula.list
sudo apt-get update -y
sudo apt-get -y install opennebula-node-kvm
sudo systemctl restart libvirtd
```


***03-Get both, Frontend and KVM Node Cloud for evaluation ---> run on evaluation node***

 Run the following commands to deploy an evaluation cloud with a front-end and a single KVM node:

```
sudo apt-get update -y
sudo apt-get upgrade -y
wget 'https://github.com/OpenNebula/minione/releases/latest/download/minione'
sudo bash minione
```
****
**Important Note!** 

After Install opennebula on each node, The oneadmin user is automatically created on each node,
which must have its own node access, and become a member of the **oneadmin** group, For example:

```
sudo su -
chown -R oneadmin:oneadmin /var/lib/one/.ssh 
```
****

***make sure the servers have passwordless authentication, We create passwordless authentication with below codes:***

****

***Add hostnames to all nodes, like below example:***

```
sudo nano /etc/hostname

192.168.200.50 frontend
192.168.200.51 kvm01
192.168.200.52 storage

```


**Very Important Note!** 

Make sure that authenticated keys created by **oneadmin** user and exists on **/var/lib/one/.ssh** folder on compute host (kvm01) 

- 01 - Goto kvm01 host and run:

```
sudo su -
su - oneadmin
ssh-keygen -t rsa -b 2048

cd /var/lib/one/.ssh
touch authorized_keys

chown -R oneadmin:oneadmin /var/lib/one/.ssh

cat id_rsa.pub
# copy generated output to auhorized_keys file on {kvm01/var/lib/one/.ssh} to {frontend/var/lib/one/.ssh} with oneadmin permission

```

copy id_rsa.pub {kvm01} ---->to-----> {forntend}--------> authorized_keys
****
***Copy generated keys on each node***

- 02 - Goto frontend host and run:

```
sudo su -
su - oneadmin
cd /var/lib/one/.ssh/authorized_keys
cat id_rs.pub
# copy generated output to auhorized_keys file on {fronend node/var/lib/one/.ssh} to {kvm01/var/lib/one/.ssh} with oneadmin permission
```
copy id_rsa.pub {fronend node} ---->to-----> {kvm01}--------> authorized_keys



















