


rm /etc/machine-id
touch /etc/machine id





disable cloud init ubuntu



How to disable cloud-init in Ubuntu
Prevent start

    Create an empty file to prevent the service from starting

      sudo touch /etc/cloud/cloud-init.disabled

Uninstall

    Disable all services (uncheck everything except "None"):

      sudo dpkg-reconfigure cloud-init

    Uninstall the package and delete the folders

      sudo dpkg-reconfigure cloud-init
      sudo apt-get purge cloud-init
      sudo rm -rf /etc/cloud/ && sudo rm -rf /var/lib/cloud/

    Restart the computer

      sudo reboot


apt --fix-broken install
wget https://github.com/OpenNebula/addon-context-linux/releases/download/v6.6.1/one-context_6.6.1-1.deb
dpkg -i one-context_6.6.1-1.deb

apt autoremove

rm /etc/machine-id
touch /etc/machine id


cat /dev/null > ~/.bash_history && history -c -w && exit
