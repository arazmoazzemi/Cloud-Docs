# Install openstack with kolla-ansible:

- ***[kolla-ansible-latest](https://docs.openstack.org/kolla-ansible/latest/)***

- ***[quickstart-guide](https://docs.openstack.org/kolla-ansible/latest/user/quickstart.html)***


### Host machine requirements:

- ***2 network interfaces***

- ***8GB main memory***

- ***40GB disk space***


Let's go:

```bash

sudo apt update -y
sudo apt upgrade -y
sudo apt install git python3-dev libffi-dev gcc libssl-dev -y
sudo apt install python3-venv -y

python3 -m venv ./openstack
source openstack/bin/activate

pip install -U pip
pip install 'ansible>=6,<8'
pip install git+https://opendev.org/openstack/kolla-ansible@master

ls openstack/share/kolla-ansible/


sudo mkdir -p /etc/kolla
sudo chown $USER:$USER /etc/kolla

cp -r /root/openstack/share/kolla-ansible/etc_examples/kolla/* /etc/kolla
cp  openstack/share/kolla-ansible/ansible/inventory/all-in-one .

cat all-in-one

```

### Install Ansible Galaxy requirements:

```bash
kolla-ansible install-deps

# Configuration

kolla-genpwd
cat /etc/kolla/passwords.yml

kolla_base_distro: "rocky"

openstack_tag_suffix: "-aarch64"

network_interface: "eth0"

neutron_external_interface: "eth1"

kolla_internal_vip_address: "10.1.0.250"

```


































