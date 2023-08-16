# WORDPRESS CONTEXT

```
CONTEXT = [
  NETWORK = "YES",
  ONEAPP_ADMIN_EMAIL = "$ONEAPP_ADMIN_EMAIL",
  ONEAPP_ADMIN_PASSWORD = "$ONEAPP_ADMIN_PASSWORD",
  ONEAPP_ADMIN_USERNAME = "$ONEAPP_ADMIN_USERNAME",
  ONEAPP_SITE_TITLE = "$ONEAPP_SITE_TITLE",
  ONEAPP_SSL_CERT = "$ONEAPP_SSL_CERT",
  ONEAPP_SSL_CHAIN = "$ONEAPP_SSL_CHAIN",
  ONEAPP_SSL_PRIVKEY = "$ONEAPP_SSL_PRIVKEY",
  PASSWORD = "XQXgmnf2qr6H4iFnwHhM0w==",
  SSH_PUBLIC_KEY = "$USER[SSH_PUBLIC_KEY]",
  START_SCRIPT = "
  sed -i -e 's/.*PasswordAuthentication .*/PasswordAuthentication yes/' /etc/ssh/sshd_config&& sed -i -e 
  's/.*PermitRootLogin .*/PermitRootLogin yes/' 
  /etc/ssh/sshd_config&& sed -i -e 's/.*UseDNS .*/UseDNS no/' /etc/ssh/sshd_config&& systemctl restart sshd",
  USERNAME = "root" ]
CPU = "1"
DISK = [
  IMAGE_ID = "3" ]
GRAPHICS = [
  LISTEN = "0.0.0.0",
  TYPE = "VNC" ]
HOT_RESIZE = [
  CPU_HOT_ADD_ENABLED = "NO",
  MEMORY_HOT_ADD_ENABLED = "NO" ]
HYPERVISOR = "kvm"
INPUTS_ORDER = "ONEAPP_SSL_CERT,ONEAPP_SSL_PRIVKEY,ONEAPP_SSL_CHAIN,ONEAPP_SITE_TITLE,ONEAPP_ADMIN_USERNAME,ONEAPP_ADMIN_EMAIL,ONEAPP_ADMIN_PASSWORD"
MEMORY = "1024"
MEMORY_RESIZE_MODE = "BALLOONING"
MEMORY_UNIT_COST = "MB"
NIC = [
  NETWORK = "vnet",
  NETWORK_UNAME = "oneadmin",
  SECURITY_GROUPS = "0" ]
OS = [
  ARCH = "x86_64",
  FIRMWARE = "",
  FIRMWARE_SECURE = "YES" ]
USER_INPUTS = [
  ONEAPP_ADMIN_EMAIL = "O|text|** Site Administrator E-mail (set all or none)| |",
  ONEAPP_ADMIN_PASSWORD = "O|password|** Site Administrator Password (set all or none)",
  ONEAPP_ADMIN_USERNAME = "O|text|** Site Administrator Login (set all or none)| |",
  ONEAPP_SITE_TITLE = "O|text|** Site Title (set all or none)| |",
  ONEAPP_SSL_CERT = "O|text64|SSL certificate| |",
  ONEAPP_SSL_CHAIN = "O|text64|SSL CA chain| |",
  ONEAPP_SSL_PRIVKEY = "O|text64|SSL private key| |" ]
VCPU = "2"
```
