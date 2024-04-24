opennebula Using the Docker Hub Marketplace

curl -L https://github.com/docker/machine/releases/download/v0.16.2/docker-machine-`uname -s`-`uname -m` >/tmp/docker-machine &&
    chmod +x /tmp/docker-machine &&
    sudo cp /tmp/docker-machine /usr/local/bin/docker-machine


opennebula Using the Docker Hub Marketplace

apt-get install docker-machine-opennebula




export ONE_AUTH=~/.one/one_auth
export ONE_XMLRPC=http://192.168.200.20:2633/RPC2



TEMPLATE_ID=8
VM_NAME=nextcloud


docker-machine create --driver opennebula --opennebula-template-id $TEMPLATE_ID $VM_NAME

docker-machine create --driver opennebula --opennebula-network-name $NETWORK_NAME --opennebula-image-id $BOOT2DOCKER_IMG_ID --opennebula-b2d-size $DATA_SIZE_MB b2d

docker-machine ls



