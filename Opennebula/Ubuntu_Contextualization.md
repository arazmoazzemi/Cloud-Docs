CONTEXT = [
  NETWORK = "YES",
  USERNAME = root,
  PASSWORD = password,
  REPORT_READY = "YES",
  START_SCRIPT = "
sed -i -e 's/.*PasswordAuthentication .*/PasswordAuthentication yes/' /etc/ssh/sshd_config&& sed -i -e 's/.*PermitRootLogin .*/PermitRootLogin yes/' 
/etc/ssh/sshd_config&& sed -i -e 's/.*UseDNS .*/UseDNS no/' /etc/ssh/sshd_config&& systemctl restart sshd" ]
CPU = "2"
DISK = [
  IMAGE_ID = "1" ]
GRAPHICS = [
  LISTEN = "0.0.0.0",
  TYPE = "vnc" ]
LOGO = "images/logos/linux.png"
LXD_SECURITY_PRIVILEGED = "true"
MEMORY = "2048"
NIC = [
  NETWORK = "vnet",
  NETWORK_UNAME = "oneadmin",
  SECURITY_GROUPS = "0" ]
NIC_DEFAULT = [
  MODEL = "virtio" ]
OS = [
  ARCH = "x86_64" ]

