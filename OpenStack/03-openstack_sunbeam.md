# OpenStack sunbeam

#### [How to Install OpenStack in five simple steps | OpenStack tutorial for beginners | Ubuntu LTS](https://www.youtube.com/watch?v=ifDtBM_EHPE)

```bash
sudo apt-get update -y && sudo apt-get upgrade -y
ssh-keygen -t rsa -b 2048
```

```bash
sudo snap install openstack
sunbeam prepare-node-script | bash -x && newgrp snap_daemon
sunbeam cluster bootstrap --accept-defaults
```

```bash
snap list
```

```bash
juju controllers
juju models
juju switch openstack 
juju status
```

```bash
sudo microk8s.kubectl get namespaces
sudo microk8s.kubectl get pods -n openstack
sudo microk8s.kubectl describe pods glance-0 -n openstack
```

```bash
sunbeam openrc > admin_openrc
cat admin_openrc
source admin_openrc
```


openstack catalog list



sunbeam configure --accept-defaults --openrc demo-openrc 

sunbeam launch ubuntu -n test


----------

ssh <>

uptime
exit


sunbeam dashboard_url

cat demo-openrc












