# Install opennebula_6.8 fronend kvm ubuntu_22.04.3
#### [Docs](https://docs.opennebula.io/6.8/installation_and_configuration/frontend_installation/opennebula_repository_configuration.html)

__Install easy way__ 🙋‍♂️

#### Note! Opennebula minione way installation, needed least 30G disk or 20G free disk space for /var/ folder

* 01-Get Frontend Only ---> run on **frontend** node

```bash
sudo su -
sudo apt-get update -y
sudo apt-get upgrade -y
sudo wget 'https://github.com/OpenNebula/minione/releases/latest/download/minione'
sudo bash minione --frontend
```

* 02-Get opennebula-node-kvm only for **edge** nodes ---> Run only on **compute** node
  
```bash
sudo su -
sudo apt-get update -y
sudo apt-get upgrade -y
sudo apt-get -y install gnupg wget apt-transport-https
sudo wget -q -O- https://downloads.opennebula.io/repo/repo2.key | apt-key add -
sudo wget -q -O- https://downloads.opennebula.io/repo/repo2.key | gpg --dearmor --yes --output /etc/apt/trusted.gpg.d/opennebula.gpg
echo "deb https://downloads.opennebula.io/repo/6.8/Ubuntu/22.04 stable opennebula" > /etc/apt/sources.list.d/opennebula.list
sudo apt-get update -y
sudo apt-get -y install opennebula-node-kvm
sudo systemctl restart libvirtd
```

* 03-Get both, Frontend and KVM Node Cloud for evaluation ---> run on **evaluation** node 👨‍🎓

Run the following commands to deploy an evaluation cloud with a front-end and a single KVM node:

```bash
sudo su -
sudo apt-get update -y
sudo apt-get upgrade -y
wget 'https://github.com/OpenNebula/minione/releases/latest/download/minione'
sudo bash minione
```
****
__Important Note!__

After Install opennebula on each node, The oneadmin user is automatically created on each node,
which must have its own node access, and become a member of the **oneadmin** group, For example:

```bash
sudo su -
chown -R oneadmin:oneadmin /var/lib/one/.ssh 
```
****

__make sure the servers have passwordless authentication, We create passwordless authentication with below codes__

****

***Add hostnames to all nodes, like below example:***

```bash
sudo nano /etc/hostname

192.168.200.50 frontend
192.168.200.51 kvm01
192.168.200.52 storage

```

**Very Important Note!** Just use oneadmin keys

Make sure that authenticated keys created by **oneadmin** user and exists on **/var/lib/one/.ssh** folder on compute host (kvm01) 

* 01 - Goto kvm01 host and run:

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
after that, test this connection with : `ssh oneadmin@frontend`



copy id_rsa.pub {kvm01} ---->to-----> {forntend}--------> authorized_keys
****

***Copy generated keys on each node***

- 02 - Goto frontend host and run:

```bash
sudo su -
su - oneadmin
cd /var/lib/one/.ssh/authorized_keys
cat id_rs.pub
# copy generated output to auhorized_keys file on {fronend node/var/lib/one/.ssh} to {kvm01/var/lib/one/.ssh} with oneadmin permission
```

after that, test this connection with : `ssh oneadmin@frontend`

copy id_rsa.pub {fronend node} ---->to-----> {kvm01}--------> authorized_keys



*Make a custom bridge netwok for opennebula-kvm-node, For example:*

```bash
touch /etc/netplan/minione.yaml
nano /etc/netplan/minione.yaml

# add below codes:

network:
  version: 2
  renderer: networkd
  ethernets:
    minionebr-nic: {}
  bridges:
    minionebr:
      optional:
        true
      addresses: [ 172.16.100.1/24 ]
      interfaces: [ minionebr-nic ]


sudo netplan apply

```

*Make sure that enabled port forwarding:*

```bash
sudo echo -e '\n#Enable IP Routing\nnet.ipv4.ip_forward = 1' | sudo tee -a /etc/sysctl.conf
sudo sysctl -p
```

*Enable Nat for minione interface*

```bash
sudo iptables -F
sudo iptables -L -v -n | more

# check "netfilter-persistent save" "Saving iptables changes"
sudo apt-get -y install iptables-persistent
sudo netfilter-persistent save
sudo systemctl enable netfilter-persistent

sudo iptables -t nat -A POSTROUTING -o ens32 -j MASQUERADE
sudo iptables -A FORWARD -i ens32 -o minionebr -m state --state RELATED,ESTABLISHED -j ACCEPT
sudo iptables -A FORWARD -i minionebr -o ens32 -j ACCEPT

```

*Context example for ubuntu22.04 images*

```bash
CONTEXT = [
  NETWORK = "YES",
  USERNAME = root,
  PASSWORD = password,
  REPORT_READY = "YES",
  START_SCRIPT = "
sed -i -e 's/.*PasswordAuthentication .*/PasswordAuthentication yes/' /etc/ssh/sshd_config&& sed -i -e 's/.*PermitRootLogin .*/PermitRootLogin yes/' 
/etc/ssh/sshd_config&& sed -i -e 's/.*UseDNS .*/UseDNS no/' /etc/ssh/sshd_config&& systemctl restart sshd" ]
CPU = "2"
DISK = [
  IMAGE_ID = "1" ]
GRAPHICS = [
  LISTEN = "0.0.0.0",
  TYPE = "vnc" ]
LOGO = "images/logos/linux.png"
LXD_SECURITY_PRIVILEGED = "true"
MEMORY = "2048"
NIC = [
  NETWORK = "vnet",
  NETWORK_UNAME = "oneadmin",
  SECURITY_GROUPS = "0" ]
NIC_DEFAULT = [
  MODEL = "virtio" ]
OS = [
  ARCH = "x86_64" ]

```

### Note! After install and update images if face with below info:

- ***A start job is running for wait for network to be configured.***
```bash
sudo systemctl disable NetworkManager-wait-online.service
sudo systemctl mask systemd-networkd-wait-online.service
```





