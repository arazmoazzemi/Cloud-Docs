

```
----------------------------Login Page---------------------------------------------------
# upload path
/usr/lib/one/sunstone/public/images

# add path to below
nano  /usr/lib/one/sunstone/views/login.erb

background: url(<%=$views_config.logo%>) no-repeat center;
background: url(https://cloud.cesga.es/images/CESGA_BG.jpg) no-repeat center center fixed;
















--------------------------------------VM Template Logos--------------------------------------
# https://docs.vonecloud.today/2.0/appliance_configuration/advanced_customizations.html

download svg or png file
logo size must be == >  90 x 96 pixel

upload logos below folders paths:

/usr/lib/one/sunstone/public/images/logos
/usr/lib/one/fireedge/dist/client/assets/images/logos/

chmod 644 /usr/lib/one/fireedge/dist/client/assets/images/logos/wordpress.png

# fireedge
LOGO                 /assets/images/logos/moodle.png

you should be set logs configurations from old opennebula panel vm templates (without fireedge)



Change the the LOGO= line to LOGO="images/logos/<mylogo>.png.

add below samples to sunstone-logos.yaml
nano /etc/one/sunstone-logos.yaml

# You can add custom logos here, or disable any of the default ones commenting
# out its line
- { 'name': "Alpine Linux",    'path': "images/logos/alpine.png"}
- { 'name': "ALT",             'path': "images/logos/alt.png"}
- { 'name': "Arch Linux",      'path': "images/logos/arch.png"}
- { 'name': "CentOS",          'path': "images/logos/centos.png"}
- { 'name': "Debian",          'path': "images/logos/debian.png"}
- { 'name': "Fedora",          'path': "images/logos/fedora.png"}
- { 'name': "FreeBSD",         'path': "images/logos/freebsd.png"}
- { 'name': "HardenedBSD",     'path': "images/logos/hardenedbsd.png"}
- { 'name': "Knoppix",         'path': "images/logos/knoppix-logo.png"}
- { 'name': "Linux",           'path': "images/logos/linux.png"}
- { 'name': "Oracle",          'path': "images/logos/oel.png"}
- { 'name': "Redhat",          'path': "images/logos/redhat.png"}
- { 'name': "SUSE",            'path': "images/logos/suse.png"}
- { 'name': "Ubuntu",          'path': "images/logos/ubuntu.png"}
- { 'name': "Windows XP/2003", 'path': "images/logos/windowsxp.png"}
- { 'name': "Windows 8/2012",  'path': "images/logos/windows8.png"}
- { 'name': "Windows 10/2016", 'path': "images/logos/windows8.png"}
- { 'name': "canvaslms",       'path': "images/logos/canvaslms.png"}
- { 'name': "grafana",         'path': "images/logos/grafana.png"}
- { 'name': "jenkins",         'path': "images/logos/jenkins.png"}
- { 'name': "mysql",           'path': "images/logos/mysql.png"}
- { 'name': "postgresql",      'path': "images/logos/postgresql.png"}
- { 'name': "redis",           'path': "images/logos/redis.png"}
- { 'name': "roundcube",       'path': "images/logos/roundcube.png"}
- { 'name': "zabbix",          'path': "images/logos/zabbix.png"}
- { 'name': "moodle",          'path': "images/logos/moodle.png"}
- { 'name': "ttylinux",        'path': "images/logos/ttylinux.png"}
- { 'name': "wordpress",       'path': "images/logos/wordpress.png"}
- { 'name': "resourcespace",   'path': "images/logos/resourcespace.png"}
- { 'name': "memcached",       'path': "images/logos/memcached.png"}
- { 'name': "gitlab-ce",       'path': "images/logos/gitlab-ce.png"}
- { 'name': "kafka",           'path': "images/logos/kafka.png"}
- { 'name': "jupyterhub",      'path': "images/logos/jupyterhub.png"}
- { 'name': "clickhouse",      'path': "images/logos/clickhouse.png"}
- { 'name': "mariadb",         'path': "images/logos/mariadb.png"}
- { 'name': "minio",           'path': "images/logos/minio.png"}
- { 'name': "typo3",           'path': "images/logos/typo3.png"}
- { 'name': "tinytinyrss",     'path': "images/logos/tinytinyrss.png"}
- { 'name': "subversion",      'path': "images/logos/subversion.png"}
- { 'name': "sonarqube",       'path': "images/logos/sonarqube.png"}
- { 'name': "silverstripe",    'path': "images/logos/silverstripe.png"}
- { 'name': "redmine",         'path': "images/logos/redmine.png"}
- { 'name': "rabbitmq",        'path': "images/logos/rabbitmq.png"}
- { 'name': "prestashop",      'path': "images/logos/prestashop.png"}
- { 'name': "percona-mysql",   'path': "images/logos/percona-mysql.png"}
- { 'name': "openfire",        'path': "images/logos/openfire.png"}
- { 'name': "opencart",        'path': "images/logos/opencart.png"}
- { 'name': "odoo",            'path': "images/logos/odoo.png"}
- { 'name': "mongodb",         'path': "images/logos/mongodb.png"}
- { 'name': "mariadb",         'path': "images/logos/mariadb.png"}
- { 'name': "livehelperchat",  'path': "images/logos/livehelperchat.png"}
- { 'name': "lamp",            'path': "images/logos/lamp.png"}
- { 'name': "kong",            'path': "images/logos/kong.png"}
- { 'name': "jaeger",          'path': "images/logos/jaeger.png"}
- { 'name': "influxdb",        'path': "images/logos/influxdb.png"}
- { 'name': "guacamole",       'path': "images/logos/guacamole.png"}
- { 'name': "erpnext",         'path': "images/logos/erpnext.png"}
- { 'name': "ejbca",           'path': "images/logos/ejbca.png"}
- { 'name': "elasticsearch",   'path': "images/logos/elasticsearch.png"}
- { 'name': "concrete5",       'path': "images/logos/concrete5.png"}
- { 'name': "cassandra",       'path': "images/logos/cassandra.png"}
- { 'name': "activemq",        'path': "images/logos/activemq.png"}








LOGO = "images/logos/canvas.png"



- { 'name': "canvas", 'path': "images/logos/canvas.png"}
- { 'name': "grafana", 'path': "images/logos/grafana.png"}
- { 'name': "jenkins", 'path': "images/logos/jenkins.png"}
- { 'name': "mysql", 'path': "images/logos/mysql.png"}
- { 'name': "postgresql", 'path': "images/logos/postgresql.png"}
- { 'name': "redis", 'path': "images/logos/redis.png"}
- { 'name': "roundcube", 'path': "images/logos/roundcube.png"}
- { 'name': "zabbix", 'path': "images/logos/zabbix.png"}
- { 'name': "moodle", 'path': "images/logos/moodle.png"}
- { 'name': "ttylinux", 'path': "images/logos/ttylinux.png"}
- { 'name': "wordpress", 'path': "images/logos/wordpress.png"}
- { 'name': "resourcespace", 'path': "images/logos/resourcespace.png"}
- { 'name': "memcached", 'path': "images/logos/resourcespace.png"}

```




































