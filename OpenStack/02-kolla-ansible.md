# Install openstack with kolla-ansible:

- ***[kolla-ansible-latest](https://docs.openstack.org/kolla-ansible/latest/)***

- ***[quickstart-guide](https://docs.openstack.org/kolla-ansible/latest/user/quickstart.html)***


### Host machine requirements

***2 network interfaces***

***8GB main memory***

***40GB disk space***



sudo apt update

sudo apt install git python3-dev libffi-dev gcc libssl-dev


sudo apt install python3-venv



python3 -m venv /path/to/venv
source /path/to/venv/bin/activate


pip install -U pip



pip install 'ansible>=6,<8'


pip install git+https://opendev.org/openstack/kolla-ansible@master


sudo mkdir -p /etc/kolla
sudo chown $USER:$USER /etc/kolla



cp -r /path/to/venv/share/kolla-ansible/etc_examples/kolla/* /etc/kolla


cp /path/to/venv/share/kolla-ansible/ansible/inventory/all-in-one .



