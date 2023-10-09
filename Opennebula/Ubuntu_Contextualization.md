# Ubuntu Contextualization Example:

```
CONTEXT = [
  NETWORK = "YES",
  PASSWORD = "password",
  REPORT_READY = "YES",
  USERNAME = "root" ]
CPU = "2"
DISK = [
  IMAGE_ID = "1" ]
GRAPHICS = [
  LISTEN = "0.0.0.0",
  TYPE = "VNC" ]
HOT_RESIZE = [
  CPU_HOT_ADD_ENABLED = "NO",
  MEMORY_HOT_ADD_ENABLED = "NO" ]
HYPERVISOR = "kvm"
LOGO = "images/logos/linux.png"
LXD_SECURITY_PRIVILEGED = "true"
MEMORY = "2048"
MEMORY_RESIZE_MODE = "BALLOONING"
MEMORY_UNIT_COST = "MB"
NIC = [
  NETWORK = "vnet",
  NETWORK_UNAME = "oneadmin",
  SECURITY_GROUPS = "0" ]
NIC_DEFAULT = [
  MODEL = "virtio" ]
OS = [
  ARCH = "x86_64",
  FIRMWARE = "",
  FIRMWARE_SECURE = "YES" ]
VCPU = "2"


```
