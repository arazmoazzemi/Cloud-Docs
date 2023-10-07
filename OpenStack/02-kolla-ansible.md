# Install openstack with kolla-ansible:

- ***[kolla-ansible-developers](https://docs.openstack.org/kolla-ansible/latest/user/quickstart-development.html)***

- ***[kolla-ansible-latest](https://docs.openstack.org/kolla-ansible/latest/)***

- ***[quickstart-guide](https://docs.openstack.org/kolla-ansible/latest/user/quickstart.html)***

#### Use below DNS for limited connections:😔
#### DNS1:  185.55.225.25 
#### DNS2:  185.55.226.26
> OR

```bash
systemctl stop systemd-resolved
systemctl mask systemd-resolved
rm /etc/resolv.conf

cat <<EOF > /etc/resolv.conf
nameserver 178.22.122.100
nameserver 185.51.200.2
EOF
``` 
##### DNS1:  10.202.10.202   
##### DNS2:  10.202.10.102

----

### Host machine requirements:

- ***2 network interfaces***

- ***8GB main memory***

- ***40GB disk space***


Let's go:

```bash

sudo apt update -y
sudo apt upgrade -y
apt-get install python3-docker -y
sudo apt install git python3-dev libffi-dev gcc libssl-dev -y
sudo apt install python3-venv -y

python3 -m venv ./openstack
source openstack/bin/activate

pip install -U pip
pip install 'ansible>=6,<8'
# pip install 'ansible>=4,<6'
pip install git+https://opendev.org/openstack/kolla-ansible@master
# git clone --branch master https://opendev.org/openstack/kolla-ansible

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
```

### Kolla passwords:
```bash
kolla-genpwd
cat /etc/kolla/passwords.yml
```

### Kolla globals.yml:
```bash
ls /etc/kolla
cp /etc/kolla/globals.yml /etc/kolla/globals.yml.orig


nano /etc/kolla/globals.yml

workaround_ansible_issue_8743: yes

kolla_base_distro: "ubuntu"

openstack_release: "zed"

kolla_internal_vip_address: "192.168.200.12"

kolla_internal_fqdn: "{{ kolla_internal_vip_address }}"

kolla_external_vip_address: "{{ kolla_internal_vip_address }}"

kolla_sysctl_conf_path: /etc/sysctl.conf

network_interface: "ens32"

network_address_family: "ipv4"

neutron_external_interface: "ens33"

neutron_plugin_agent: "ovn"

keepalived_virtual_router_id: "51"

disable_firewall: "true"

openstack_region_name: "RegionOne"

enable_openstack_core: "yes"

enable_mariadb: "yes"

enable_cinder: "yes"

enable_cinder_backup: "yes"

enable_cinder_backend_lvm: "yes"

glance_backend_ceph: "yes"

cinder_volume_group: "Vg0"

cinder_backup_driver: "nfs"

cinder_backup_share: "192.168.200.12:/root/nfs"

nova_compute_virt_type: "kvm"

nova_console: "spice"

neutron_ovn_distributed_fip: "yes"

neutron_ovn_dhcp_agent: "yes"

```

----

### Create a volume group
```bash
vgcreate vg0 /dev/sdb
```

----

# Deployment:

```bash
kolla-ansible -i ./all-in-one bootstrap-servers
```

# If get error with firewall deactive env and run:

```bash
ufw enable
source openstack/bin/activate

kolla-ansible -i ./all-in-one bootstrap-servers
```

```bash
kolla-ansible -i ./all-in-one prechecks
```

```bash
kolla-ansible -i ./all-in-one deploy
```





























