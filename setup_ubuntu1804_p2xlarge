#!/bin/bash
###
# setup machine learning env on ec2
# requires:
#   - ubuntu18.04
#   - gpu instance (p2.xlarge)
# if you can't use docker command without sudo after executing this script, 
# please exit and re-login.
###

# Install docker
sudo apt-get update
sudo apt-get install -y docker.io
sudo gpasswd -a ubuntu docker

# Instal other tools
sudo apt-get install -y git vim

# Install nvidia driver
# https://docs.nvidia.com/datacenter/tesla/tesla-installation-notes/index.html
sudo apt-get install linux-headers-$(uname -r)
distribution=$(. /etc/os-release;echo $ID$VERSION_ID | sed -e 's/\.//g')
wget https://developer.download.nvidia.com/compute/cuda/repos/$distribution/x86_64/cuda-$distribution.pin
sudo mv cuda-$distribution.pin /etc/apt/preferences.d/cuda-repository-pin-600
sudo apt-key adv --fetch-keys https://developer.download.nvidia.com/compute/cuda/repos/$distribution/x86_64/7fa2af80.pub
echo "deb http://developer.download.nvidia.com/compute/cuda/repos/$distribution/x86_64 /" | sudo tee /etc/apt/sources.list.d/cuda.list
sudo apt-get update
sudo apt-get -y install cuda-drivers

# Install nvidia-container-toolkit
# https://github.com/NVIDIA/nvidia-docker
distribution=$(. /etc/os-release;echo $ID$VERSION_ID)
curl -s -L https://nvidia.github.io/nvidia-docker/gpgkey | sudo apt-key add -
curl -s -L https://nvidia.github.io/nvidia-docker/$distribution/nvidia-docker.list | sudo tee /etc/apt/sources.list.d/nvidia-docker.list
sudo apt-get update && sudo apt-get install -y nvidia-container-toolkit
sudo systemctl restart docker

# Finish!
echo '==========================================='
echo '= setup finish! please exit and re-login. ='
echo '==========================================='
