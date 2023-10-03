### Install opennebula 6.7 (❁´◡`❁)  on ubuntu 22.04.3 ❤

----
Note! Befor start your stup, Please enable nested virtualization on your host😊

- Lets start:

```bash
apt-get update -y
apt-get upgrade -y

apt-get -y install gnupg wget apt-transport-https
wget -q -O- https://downloads.opennebula.io/repo/repo2.key | apt-key add -
echo "deb https://downloads.opennebula.io/repo/6.7/Ubuntu/22.04 stable opennebula" > /etc/apt/sources.list.d/opennebula.list
apt-get update -y

apt-get -y install opennebula opennebula-sunstone opennebula-fireedge opennebula-gate opennebula-flow opennebula-provision

systemctl start opennebula opennebula-sunstone opennebula-fireedge opennebula-gate opennebula-flow
systemctl enable opennebula opennebula-sunstone opennebula-fireedge 

# show password
cat /var/lib/one/.one/one_auth

username: oneadmin
password : <# show password>

default ports: 

# For example:
# http://192.168.200.40:9869/ ----> Frontend
# http://192.168.200.40:2616/ ---->FireEdge


```

- FireEdge configuration:🔥 

```bash
nano /etc/one/sunstone-server.conf

http://<OPENNEBULA-FRONTEND-IP-ADDRESS>:2616
```




---------------

apt-get -y install opennebula-node-kvm
	

su - oneadmin
ssh-copy-id -i /var/lib/one/.ssh/id_rsa.pub cloud
scp -p /var/lib/one/.ssh/id_rsa <node1>:/var/lib/one/.ssh/



------------------

sudo iptables -F
sudo iptables -L -v -n | more

# check "netfilter-persistent save" "Saving iptables changes"
sudo apt-get -y install iptables-persistent
sudo netfilter-persistent save
sudo systemctl enable netfilter-persistent

sudo iptables -t nat -A POSTROUTING -o ens33 -j MASQUERADE
sudo iptables -A FORWARD -i ens33 -o minionebr -m state --state RELATED,ESTABLISHED -j ACCEPT
sudo iptables -A FORWARD -i minionebr -o ens33 -j ACCEPT



--------------

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

--------

CONTEXT = [
  NETWORK = "YES",
  PASSWORD = "3VoKHaXpIZoj0oHAvL6rWA==",
  REPORT_READY = "YES",
  USERNAME = "root" ]
CPU = "2"
DISK = [
  IMAGE_ID = "1" ]
GRAPHICS = [
  LISTEN = "0.0.0.0",
  TYPE = "VNC" ]
HOT_RESIZE = [
  CPU_HOT_ADD_ENABLED = "NO",
  MEMORY_HOT_ADD_ENABLED = "NO" ]
HYPERVISOR = "kvm"
LOGO = "images/logos/linux.png"
LXD_SECURITY_PRIVILEGED = "true"
MEMORY = "2048"
MEMORY_RESIZE_MODE = "BALLOONING"
MEMORY_UNIT_COST = "MB"
NIC = [
  NETWORK = "vnet",
  NETWORK_UNAME = "oneadmin",
  SECURITY_GROUPS = "0" ]
NIC_DEFAULT = [
  MODEL = "virtio" ]
OS = [
  ARCH = "x86_64",
  FIRMWARE = "",
  FIRMWARE_SECURE = "YES" ]
VCPU = "2"


