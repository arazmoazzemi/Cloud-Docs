### Install opennebula 6.8 (❁´◡`❁)  on ubuntu 22.04.3 ❤

----
### Important Note! Before start your steps to stup, Please enable nested virtualization on your host😊
----
Also,
### You can use chrony and set local timezone

#### - Let's start:

```bash
sudo apt-get update -y
sudo apt-get upgrade -y

sudo ssh-keygen -t rsa -b 2048

sudo apt-get -y install gnupg wget apt-transport-https
sudo wget -q -O- https://downloads.opennebula.io/repo/repo2.key | apt-key add -
sudo echo "deb https://downloads.opennebula.io/repo/6.8/Ubuntu/22.04 stable opennebula" > /etc/apt/sources.list.d/opennebula.list
sudo apt-get update -y

sudo apt-get -y install opennebula opennebula-sunstone opennebula-fireedge opennebula-gate opennebula-flow opennebula-provision

sudo systemctl start opennebula opennebula-sunstone opennebula-fireedge opennebula-gate opennebula-flow
sudo systemctl enable opennebula opennebula-sunstone opennebula-fireedge 

# show password
cat /var/lib/one/.one/one_auth

username: oneadmin
password : <# show password>

default ports: 

# For example:
# http://192.168.200.40:9869/ ----> Frontend
# http://192.168.200.40:2616/ ---->FireEdge

```

#### - FireEdge configuration:🔥 

```bash
nano /etc/one/sunstone-server.conf
http://<OPENNEBULA-FRONTEND-IP-ADDRESS>:2616

systemctl restart opennebula opennebula-sunstone opennebula-fireedge
```

----
#### - Install KVM node:

```bash
apt-get -y install opennebula-node-kvm
	
# su - oneadmin
# ssh-copy-id -i /var/lib/one/.ssh/id_rsa.pub cloud
# scp -p /var/lib/one/.ssh/id_rsa <node1>:/var/lib/one/.ssh/

```
----

#### - Add KVMnode with CLI:

```bash
onehost create <node01> -i kvm -v kvm
```

#### - Make sure that enabled port forwarding:

```bash
sudo echo -e '\n#Enable IP Routing\nnet.ipv4.ip_forward = 1' | sudo tee -a /etc/sysctl.conf
sudo sysctl -p
```

----

- Create a bidge network:

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

# Apply network changes
sudo netplan apply
```

- Enable Nat for minione interface:

```bash
sudo iptables -F
sudo iptables -L -v -n | more

# check "netfilter-persistent save" "Saving iptables changes"
sudo apt-get -y install iptables-persistent
sudo netfilter-persistent save
sudo systemctl enable netfilter-persistent

# Change with your right interfaces:

sudo iptables -t nat -A POSTROUTING -o ens33 -j MASQUERADE
sudo iptables -A FORWARD -i ens33 -o minionebr -m state --state RELATED,ESTABLISHED -j ACCEPT
sudo iptables -A FORWARD -i minionebr -o ens33 -j ACCEPT

```


- Virtual network context

```bash
NAME         = "Private"
VN_MAD       = "bridge"
BRIDGE       = minionebr
DESCRIPTION  = "A private network for VM inter-communication"

#Address Ranges, only these addresses will be assigned to the VMs
AR=[
    TYPE = "IP4",
    IP   = "172.16.100.2",
    SIZE = "100"
]


# Context attributes
NETWORK_ADDRESS    = "172.16.100.0"
NETWORK_MASK       = "255.255.255.0"
GATEWAY            = "172.16.100.1"
DNS                = "8.8.8.8"
SEARCH_DOMAIN      = "example.com"
```

----

- Ubuntu VM context:

```bash
CONTEXT = [
  NETWORK = "YES",
  PASSWORD = "ubuntu",
  REPORT_READY = "YES",
  USERNAME = "root" ]
CPU = "2"
DISK = [
  IMAGE = "Ubuntu 22.04",
  IMAGE_UNAME = "oneadmin" ]
GRAPHICS = [
  LISTEN = "0.0.0.0",
  TYPE = "VNC" ]
HOT_RESIZE = [
  CPU_HOT_ADD_ENABLED = "NO",
  MEMORY_HOT_ADD_ENABLED = "NO" ]
HYPERVISOR = "kvm"
LOGO = "images/logos/ubuntu.png"
LXD_SECURITY_PRIVILEGED = "true"
MEMORY = "2048"
MEMORY_RESIZE_MODE = "BALLOONING"
MEMORY_UNIT_COST = "MB"
NIC = [
  NETWORK = "Private",
  NETWORK_UNAME = "oneadmin",
  SECURITY_GROUPS = "0" ]
NIC_DEFAULT = [
  MODEL = "virtio" ]
OS = [
  ARCH = "x86_64",
  FIRMWARE = "",
  FIRMWARE_SECURE = "YES" ]
SCHED_DS_REQUIREMENTS = "ID=\"0\""
VCPU = "2"

```
----

USERNAME: root

PASSWORD: ubuntu

----

LVM disk resize

```bash
pvresize /dev/vda3

lvextend -l +100%FREE /dev/ubuntu-vg/ubuntu-lv

resize2fs /dev/mapper/ubuntu--vg-ubuntu--lv

```
