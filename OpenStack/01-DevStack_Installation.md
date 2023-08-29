# Devstack, Latest Installation

----

All-In-One or OpenStack AIO:

DevStack and Packstack

Openstack-Ansible

SaltStack OpenStack

Puppet







6️⃣ نصب OpenStack از طریق Puppet



7️⃣ نصب OpenStack از طریق Chef 



📌 توجه: ابزارهای SaltStack و Puppent و Check هم مثل ابزار Ansible یک ساختار Client/Serverی دارند و از طریق یک automation configuration file پیکربندی شده شبیه به playbookها در Ansible، پیکربندی های را بر روی سرورها اعمال می کنند.



♻️ نصب و راه اندازی Open Stack در محیط های Containerization



8️⃣ نصب OpenStack توسط Kolla

ممکن است شما نیاز به نصب OpenStack در محیط های Conternization همچون Docker داشته باشید. برای این منظور یک Community Open Source به نام Kolla یکسری containerهای آماده و از پیش ساخته شده برای نصب OpenStack در Docker به همراه یکسری ابزارها از جمله Kolla-Ansible (جهت فرهم کردن Ansible playbookها و پیاده سازی Kolla imageها)، Kayobe (ابزاری می تواند برای شما containerهای OpenStack را به صورت bare metal با استفاده از Kolla و Kolla Ansible و Bifrosft پیاده سازی نماید) را ارائه نموده است.



9️⃣ نصب OpenStack توسط OpenStack-Helm

در صورتیکه شما از محیط Google’s Kubernetes و کلاسترهای آن استفاده می نمایید، یک Community Open Source به اسم OpenStack-Helm برای شما نصب OpenStack و سرویس های آن را در این محیط تسهیل کرده است.



No alt text provided for this image
♻️ سایر روش های نصب و راه اندازی OpenStack



🔟 نصب OpenStack از طریق TripleO

در واقع TripleO یکی از راهکارهای Community معروف RDO است که محصول Packstack را نیز ارائه کرده است. TripleO بع معنی OpenStack-On-OpenStack بوده و با هدف نصب، بروزرسانی و عملیاتی کردن OpenStack Cloudها بر روی خود OpenStack Cloud توسعه داده شده است. این مدل از پیاده سازی OpenStack دارای معماری خاص خود است و نیازمند راه اندازی Undercloud (یک operator واقعی جهت پیاده سازی Cloud) شامل کامپوننت های اصلی OpenStack از جمله Nova و Neutron و Heat و... به صورت اتوماتیک و پیاده سازی و مدیریت یک Overcloud (یک tenant واقعی از workload cloud) می باشد. در واقع Overcloud عملیات deploy کردن solution و ارائه یک Cloud با اهداف مختلف (از جمله Production و Test و...) را برعهده دارد. همچنین operator نیز می تواند هر یک از Overcloud Roleهای موجود (از جمله: controller و compute و...) را که می خواهد آنها را در محیط پیاده سازی نماید، انتخاب کند.



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





