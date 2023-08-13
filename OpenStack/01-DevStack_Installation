#Latest Installation wirh devstack

#https://docs.openstack.org/devstack/latest/guides/single-machine.html

```
sudo useradd -s /bin/bash -d /opt/stack -m stack

sudo chmod +x /opt/stack

apt-get install sudo -y || yum install -y sudo
echo "stack ALL=(ALL) NOPASSWD: ALL" | sudo tee /etc/sudoers.d/stack


sudo passwd stack <secret>
```


*Note! From here on you should use the user you created. Logout and login as that user:*

```
sudo apt-get install git -y || sudo yum install -y git
git clone https://opendev.org/openstack/devstack
cd devstack


nano local.conf


[[local|localrc]]
FLOATING_RANGE=192.168.1.224/27
FIXED_RANGE=10.11.12.0/24
ADMIN_PASSWORD=supersecret
DATABASE_PASSWORD=iheartdatabases
RABBIT_PASSWORD=flopsymopsy
SERVICE_PASSWORD=iheartksl


./stack.sh

```





