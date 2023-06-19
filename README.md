# Open-DEK Deployment

## Pre-requisite

 - **ESP**: `20GB HD`, `4GB RAM`, `Ubuntu 20.04 LTS Server`
 - USB flash drive
 - `git`
 - `docker`
 - `docker-compose`
 - `python 3.6` or later, with the `PyYAML` module installed.

> **Note**:
> You must install Docker from the Docker repository. Installation by Docker package is not supported.

## Pre-Requisite Installation:

#### docker

```bash
sudo apt-get update
sudo apt-get upgrade

sudo apt-get install \
    ca-certificates \
    curl \
    gnupg \
    lsb-release

sudo mkdir -p /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg

echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
  $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

sudo apt-get update

sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```

#### docker-composes

```bash
# standalone docker-compose installation
sudo curl -SL https://github.com/docker/compose/releases/download/v2.18.1/docker-compose-linux-x86_64 -o /usr/local/bin/docker-compose
sudo chmod +x /usr/local/bin/docker-compose

# to verify the installation
docker compose version
```

If `docker-compose` is not installed correctly, then use this(*least recommended*):

```bash
sudo apt update
sudo apt install docker-compose
```

#### git

```bash
sudo apt install git
```

#### Python 3.6 with PyYAML

```bash
sudo apt update
sudo apt install -y python3 python3-pip
pip3 install PyYAML fqdn
```

#### Others

```bash
sudo apt install net-tools

# for searching 
sudo apt install silversearcher-ag

# to get the progress output of flashing the USB drive
sudo apt install pv 
```

## Deployment

```bash
sudo su -
git clone https://github.com/ShubhamKumar89/pwek-OpenDEK  ~/dek
cd dek/
./dek_provision.py --init-config > custom.yml
```

Copy `custom.yml` from this repo to the `custom.yml` in your system and change the `host_ip` section with your IP.

```bash
./dek_provision.py --run-esp-for-usb-boot --config=custom.yml
```
