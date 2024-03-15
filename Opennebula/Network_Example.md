### Opennebula Virtual Network Example

apt-get install bridge-utils -y
brctl addbr cloudpr

-------------------------------------
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

---------------------------------------------------




sudo iptables -t nat -A POSTROUTING -o eno1 -j MASQUERADE
sudo iptables -A FORWARD -i eno1 -o cloudpr -m state --state RELATED,ESTABLISHED -j ACCEPT
sudo iptables -A FORWARD -i cloudpr -o eno1 -j ACCEPT




----------------------Opennebula Virtual Network context--------------------------------

BRIDGE = "cloudpr"
BRIDGE_TYPE = "linux"
DNS = "8.8.8.8"
GATEWAY = "172.16.100.1"
NETWORK_ADDRESS = "172.16.100.0"
NETWORK_MASK = "255.255.255.0"
OUTER_VLAN_ID = ""
PHYDEV = ""
SECURITY_GROUPS = "0"
VLAN_ID = ""
VN_MAD = "bridge"

