# Devstack, Latest Installation

----

All-In-One or OpenStack AIO:

DevStack and Packstack

Openstack-Ansible

SaltStack OpenStack

Puppet

Chef

Containerization

Kolla / Kolla-Ansible

TripleO / OpenStack-On-OpenStack

OpenStack-Helm

Fuel OpenStack (GUI- Single node - Multi-node (non-HA) -  Multi-node (HA) )
















1️⃣1️⃣ نصب OpenStack از طریق Fuel OpenStack

ابزار Fuel یک ابزار پیاده سازی و مدیریت OpenStack به عنوان یک OpenStack community است که تجربه نصب OpenStack و پروژه ها و pluginهای مربوط به آن را به صورت GUI برای شما فراهم می کند. ابزار Fuel چندین پیکربندی پیاده سازی از پیش ساخته شده دارد که شما می توانید هر یک از آنها را بسته به نیاز خود انتخاب نموده و فوراً اقدام به پیاده سازی زیرساخت OpenStack Cloud خود نمایید. این انتخاب ها به سه صورت زیر هستند: 



 📌 حالت Single node: که نصب یک کلاستر کامل OpenStack را بر روی یک ماشین فیزیکی یا یک ماشین مجازی انجام دهید.



📌 حالت Multi-node (non-HA): که به شما اجازه نصب سرویس های اضافه OpenStack همچون Cinder و Quantum و Swift را بدون نیاز به افزایش سخت افزار و پیاده سازی قابلیت High Availability می دهد.



📌 حالت Multi-node (HA): که یک کلاستر OpenStack را با قابلیت High Availability با استفاده از سه controller node به همراه سرویس های Cinder و Quantum و Swift ایجاد می کند.



2️⃣1️⃣ نصب OpenStack با استفاده از OpenStack Autopilot

پروژه OpenStack Autopilot یکی از ساده ترین روش های نصب و راه اندازی و مدیریت یک OpenStack private cloud را برای شما فراهم می کند. این روش پیاده سازی یک OpenStack Cloud و هر چیزی که از یک Cloud انتظار دارید (از پروسه نصب تا operation) را برای شما به صورت کامل اتوماتیک سازی می کند. شما در این روش هر زمانیکه که نیاز به Scale up و Scale out کردن تجهیزات و کلاسترهای خود دارید می توانید سخت افزارها را اضافه نمایید. OpenStack Autopilot همچنین با همه vendorهای اصلی تولید کننده سرور می تواند کار کند. Autopilot همچنین قادر به استفاده از storageهای مبتنی بر تکنولوژی SDN موسوم به SDS بوده و می تواند معماری High Performance Cloud را نیز برای شما پیاده سازی نماید. بعلاوه Autopilot با یک روش بسیار ساده که شامل استفاده از Metal-as-a-Service یا به اختصار MAAS است جهت register کردن ماشین های شماست کار می کند و پیکربندی OpenStack شما را انتخاب کرده و به سخت افزارهای شما add می کند. (در واقع MAAS به شما اجازه می دهد تا رفتار physical serverهایتان شبیه به virtual machineهایتان در cloud باشد.)



3️⃣1️⃣ نصب OpenStack از Juju

در واقع Juju یک ابزار Application modeling متن باز است که به شما اجازه نصب، پیکربندی، scale و operate کردن نرم افزارهایتان در محیط های private cloud و public cloudها را می دهد. شما قادر خواهید بود تا توسط Juju تنها در چند گام اقدام به پیاده سازی و پیکربندی MAAS و سپس OpenStack Cloud از طریق آن نمایید. برای این منظور کافیست تنها دو مورد از core componentهای Juju را با استفاده MAAS پیاده سازی شده (یعنی کامپوننت Controller و Client) نصب نماییم. کامپوننت Controller در واقع یک management node برای یک محیط Cloud بوده و کامپوننت Client نیز که توسط یک operator جهت صحبت کردن با یک یا چند Controller و یا مدیریت یک یا چند محیط Cloud متفاوت مورد استفاده قرار می گیرد.














----

***https://docs.openstack.org/devstack/latest/guides/single-machine.html***

```
sudo useradd -s /bin/bash -d /opt/stack -m stack
sudo chmod +x /opt/stack
apt-get install sudo -y || yum install -y sudo
echo "stack ALL=(ALL) NOPASSWD: ALL" | sudo tee /etc/sudoers.d/stack

```


*Note! From here on you should use the user you created. Logout and login as that user:*

```
su - stack
sudo apt-get install git -y || sudo yum install -y git
git clone https://opendev.org/openstack/devstack
cd devstack

# Make a config file:
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





