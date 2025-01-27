#Setup Cloud Server#
#Everything is pre-installed on the ubuntu server#
#IN AWS WHEN SETTING UP#
#For Application and OS Images search...
Ubuntu 22.04 and choose...

###Deep Learning Base OSS Nvidia Driver GPU AMI (Ubuntu 22.04) 20250117
choose 64bit x86###

#TESTING 1/27 Deep Learning OSS Nvidia Driver AMI GPU PyTorch 2.5 (Ubuntu 22.04)

#Computer type i chose g4dn.2xlarge
#Configure storage with 200gb or more or it will run out of memory

The guide is found at:
https://nvidia.github.io/bionemo-framework/user-guide/getting-started/access-startup/

#Login and type this into command line...
__________________________________________________________



docker login nvcr.io

#username is literally: "$oauthtoken"
$oauthtoken
#Password is private API key from NVIDIA NGC account - signup online


docker pull nvcr.io/nvidia/clara/bionemo-framework:nightly

docker run --rm -it --gpus all \
  nvcr.io/nvidia/clara/bionemo-framework:nightly \
  /bin/bash

#If runs out of memory 
lsblk
#maybe expand memory in AWS and allocate that memory to the instance
  _____________________________________________

##When you see a purple box/square hit tab and then enter

sudo passwd

lsb_release -a
python3 --version
sudo apt update && sudo apt upgrade -y
sudo apt reboot
sudo apt install software-properties-common
sudo add-apt-repository ppa:deadsnakes/ppa
sudo apt install python3.9
sudo apt update
git clone https://github.com/NVIDIA/bionemo-framework.git     
sudo apt install software-properties-common
sudo add-apt-repository ppa:deadsnakes/ppa
sudo apt install python3.9
sudo apt update

docker run --rm -it   --gpus=all --ipc=host --ulimit memlock=-1 --ulimit stack=67108864   nvcr.io/nvidia/clara/bionemo-framework:main--nightly   /bin/bash

docker --version

curl -fsSL https://nvidia.github.io/libnvidia-container/gpgkey | sudo gpg --dearmor -o /usr/share/keyrings/nvidia-container-toolkit-keyring.gpg   && curl -s -L https://nvidia.github.io/libnvidia-container/stable/deb/nvidia-container-toolkit.list |     sed 's#deb https://#deb [signed-by=/usr/share/keyrings/nvidia-container-toolkit-keyring.gpg] https://#g' |     sudo tee /etc/apt/sources.list.d/nvidia-container-toolkit.list
sudo apt-get update
sudo apt-get install -y nvidia-container-toolkit
curl -s -L https://nvidia.github.io/libnvidia-container/stable/rpm/nvidia-container-toolkit.repo |   sudo tee /etc/yum.repos.d/nvidia-container-toolkit.repo
sudo apt update
sudo apt install dnf
sudo apt install nextgen-yum4
sudo apt update
sudo apt install zypper
sudo zypper ar https://nvidia.github.io/libnvidia-container/stable/rpm/nvidia-container-toolkit.repo
sudo nvidia-ctk runtime configure --runtime=docker
sudo systemctl restart docker
sudo docker run --rm --runtime=nvidia --gpus all ubuntu nvidia-smi
sudo apt install podman
sudo apt install ubuntu-drivers-common
sudo ubuntu-drivers autoinstall
sudo apt install nvidia-container-toolkit-base

sudo reboot

sudo nvidia-ctk cdi generate --output=/etc/cdi/nvidia.yaml  
--> ERROR failed to generate CDI spec: failed to create device CDI specs: failed to initialize NVML: Driver/library version mismatch 

sudo apt purge -s "nvidia*" "libnvidia*"
sudo apt purge "nvidia*" "libnvidia*"
sudo apt purge "cuda*" "libcuda*"
sudo apt update
sudo add-apt-repository ppa:graphics-drivers/ppa
sudo apt update
ubuntu-drivers devices

W: An error occurred during the signature verification. The repository is not updated and the previous index files will be used. GPG error: https://developer.download.nvidia.com/compute/cuda/repos/ubuntu2204/x86_64  InRelease: The following signatures couldn't be verified because the public key is not available: NO_PUBKEY A4B469963BF863CC
W: Failed to fetch https://developer.download.nvidia.com/compute/cuda/repos/ubuntu2204/x86_64/InRelease  The following signatures couldn't be verified because the public key is not available: NO_PUBKEY A4B469963BF863CC

wget https://developer.download.nvidia.com/compute/cuda/repos/ubuntu2204/x86_64/cuda-ubuntu2204.pin
sudo mv cuda-ubuntu2204.pin /etc/apt/preferences.d/cuda-repository-pin-600
wget https://developer.download.nvidia.com/compute/cuda/12.4.0/local_installers/cuda-repo-ubuntu2204-12-4-local_12.4.0-550.54.14-1_amd64.deb
sudo dpkg -i cuda-repo-ubuntu2204-12-4-local_12.4.0-550.54.14-1_amd64.deb
sudo cp /var/cuda-repo-ubuntu2204-12-4-local/cuda-*-keyring.gpg /usr/share/keyrings/
sudo apt-get update
sudo apt-get -y install cuda-toolkit-12-4

sudo apt-get install -y cuda-drivers


___________________________________
nvidia-smi
sudo nvidia-ctk cdi generate --output=/etc/cdi/nvidia.yaml  
-->nvidia-ctk: command not found
sudo apt-get install -y nvidia-container-toolkit





##################
NVIDIA Driver Instructions (choose one option)
To install the legacy kernel module flavor:

sudo apt-get install -y cuda-drivers

To install the open kernel module flavor:

sudo apt-get install -y nvidia-driver-550-opensudo apt-get install -y cuda-drivers-550

_______________________________________

sudo apt install nvidia-driver-<version>

##MAYBE TRY##
cd /usr/lib/xorg/modules/drivers/
##I dont think we used a .run installer so skip 50
#sudo /path/to/NVIDIA-Linux-x86_64-<version>.run --uninstall



sudo ubuntu-drivers autoinstall
or


sudo reboot



