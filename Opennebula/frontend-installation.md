# Install opennebula fronend kvm ubuntu22.04.2

**Install easy way**

**01-Get Frontend Only ---> run on frontend node** 


```
sudo apt-get update -y
sudo apt-get upgrade -y
wget 'https://github.com/OpenNebula/minione/releases/latest/download/minione'
sudo bash minione --frontend
```

**02-Get Frontend Only for edge nodes ---> run on compute node**
```
apt-get update
apt-get -y install gnupg wget apt-transport-https
wget -q -O- https://downloads.opennebula.io/repo/repo2.key | apt-key add -
wget -q -O- https://downloads.opennebula.io/repo/repo2.key | gpg --dearmor --yes --output /etc/apt/trusted.gpg.d/opennebula.gpg
echo "deb https://downloads.opennebula.io/repo/6.6/Ubuntu/22.04 stable opennebula" > /etc/apt/sources.list.d/opennebula.list
apt-get update
apt-get -y install opennebula-node-kvm
systemctl restart libvirtd
```


**03-Get Frontend and KVM Node Cloud for evaluation ---> run on evaluation node**

 Run the following commands to deploy an evaluation cloud with a front-end and a single KVM node:

```
sudo apt-get update -y
sudo apt-get upgrade -y
wget 'https://github.com/OpenNebula/minione/releases/latest/download/minione'
sudo bash minione
```





















