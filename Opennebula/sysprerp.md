
*Remove Machine ID:*

```bash
rm /etc/machine-id
touch /etc/machine id
```

*Disable cloud-init from ubuntu, Beacuse its maybe conflict with opennebula one-context:*

```
# Create an empty file to prevent the service from starting
sudo touch /etc/cloud/cloud-init.disabled

# Uninstall cloud-init

sudo dpkg-reconfigure cloud-init
sudo apt-get purge cloud-init
sudo rm -rf /etc/cloud/ && sudo rm -rf /var/lib/cloud/

# Restart the computer
sudo reboot
```

*Install opennebula one-context:*

```
apt --fix-broken install
wget https://github.com/OpenNebula/addon-context-linux/releases/download/v6.6.1/one-context_6.6.1-1.deb
dpkg -i one-context_6.6.1-1.deb
apt autoremove
```

*Clear bash history:*
```
# root 
sudo cat /dev/null > ~/.bash_history && history -c -w && exit
# user
cat /dev/null > ~/.bash_history && history -c -w && exit
```
