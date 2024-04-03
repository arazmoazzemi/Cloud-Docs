### Opennebula Virtual Network Example

```bash
apt-get install bridge-utils -y
brctl addbr cloudpr
```

### Create a virtual nic interface for private VMs
```bash
touch cloudpr.yaml

# This is the network config written by 'subiquity'
network:
  version: 2
  renderer: networkd
  ethernets:
    cloudpr-nic: {}
  bridges:
    cloudpr:
      optional:
        true
      addresses: [ 172.16.100.1/24 ]
      interfaces: [ cloudpr-nic ]
```

```bash
sudo apt-get -y install iptables-persistent
sudo netfilter-persistent save
sudo systemctl enable netfilter-persistent

sudo iptables -t nat -A POSTROUTING -o eno1 -j MASQUERADE
sudo iptables -A FORWARD -i eno1 -o cloudpr -m state --state RELATED,ESTABLISHED -j ACCEPT
sudo iptables -A FORWARD -i cloudpr -o eno1 -j ACCEPT
```

### Opennebula Virtual Network context
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
