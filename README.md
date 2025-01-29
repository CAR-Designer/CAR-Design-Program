#Setup Cloud Server#

GET G5 because these have A100 GPU's - theyre pretty standard GPUs and require less configuration and errors
#For Application and OS Images search...
Ubuntu 22.04 and choose...

Deep Learning OSS Nvidia Driver AMI GPU PyTorch 2.5 (Ubuntu 22.04)


#Computer type i chose g5
#Configure storage with 200gb or more or it will run out of memory

The guide is found at:
https://nvidia.github.io/bionemo-framework/user-guide/getting-started/access-startup/

#Login and type this into command line...
__________________________________________________________



#RESIZE PARTITION
lsblk
sudo apt update
sudo apt install -y parted
sudo apt upgrade
sudo parted /dev/nvme0n1
print
resizepart 1 100%
yes
quit
sudo apt update
sudo partprobe /dev/nvme0n1
df -T /
sudo resize2fs /dev/nvme0n1p1



sudo apt install containerd
sudo apt install docker.io

reboot

docker login nvcr.io

#username is literally: "$oauthtoken"
$oauthtoken
#Password is private API key from NVIDIA NGC account - signup online


docker pull nvcr.io/nvidia/clara/bionemo-framework:nightly

sudo docker run --rm --runtime=nvidia --gpus all ubuntu nvidia-smi

docker run --rm -it --gpus all nvcr.io/nvidia/clara/bionemo-framework:nightly /bin/bash


nano .env

#copy paste
# Local Cache Directories
LOCAL_RESULTS_PATH=/path/to/local/results
DOCKER_RESULTS_PATH=/path/to/docker/results
LOCAL_DATA_PATH=/path/to/local/data
DOCKER_DATA_PATH=/path/to/docker/data
LOCAL_MODELS_PATH=/path/to/local/models
DOCKER_MODELS_PATH=/path/to/docker/models

# Desired Jupyter Port
JUPYTER_PORT=8888

# NGC Configuration Settings
NGC_CLI_API_KEY=NVIDIA ACCOUNT PRIVATE KEY HERE
NGC_CLI_ORG="NVIDIA ACCOUNT NAME HERE"
NGC_CLI_TEAM=""
NGC_CLI_FORMAT_TYPE=json



#TYPE
#control+o, enter, control+x

source .env

apt-get update

MAYBE DOWNLOAD DOCKER ONTO THE BIONEMO CONTAINER?? DOCKER NOT WORKING

exit

docker run \
  --rm -it \
  --gpus all \
  --network host \
  --shm-size=4g \
  -e WANDB_API_KEY \
  -e NGC_CLI_API_KEY \
  -e NGC_CLI_ORG \
  -e NGC_CLI_TEAM \
  -e NGC_CLI_FORMAT_TYPE \
  -v $LOCAL_DATA_PATH:$DOCKER_DATA_PATH \
  -v $LOCAL_MODELS_PATH:$DOCKER_MODELS_PATH \
  -v $LOCAL_RESULTS_PATH:$DOCKER_RESULTS_PATH \
  nvcr.io/nvidia/clara/bionemo-framework:nightly \
  /bin/bash

  ____________________________________________________________________
  https://docs.nvidia.com/nim/bionemo/diffdock/latest/getting-started.html
______________________________________________________________________
  wget --content-disposition https://api.ngc.nvidia.com/v2/resources/nvidia/ngc-apps/ngc_cli/versions/3.41.3/files/ngccli_linux.zip -O ~/ngccli_linux.zip && \
unzip ~/ngccli_linux.zip -d ~/ngc && \
chmod u+x ~/ngc/ngc-cli/ngc && \
echo "export PATH=\"\$PATH:~/ngc/ngc-cli\"" >> ~/.bash_profile && source ~/.bash_profile



###FOR NGC API KEY GET NGC CLI API KEY AS SEEN HERE https://docs.nvidia.com/ngc/gpu-cloud/ngc-user-guide/index.html#generating-personal-api-key###

ngc config set

docker pull nvcr.io/nim/mit/diffdock:2.0.1


###FOR NGC API KEY GET NGC CLI API KEY AS SEEN HERE https://docs.nvidia.com/ngc/gpu-cloud/ngc-user-guide/index.html#generating-personal-api-key###

docker run --rm -it --name diffdock-nim \
  --runtime=nvidia -e NVIDIA_VISIBLE_DEVICES=0 \
  --shm-size=2G \
  --ulimit memlock=-1 \
  --ulimit stack=67108864 \
  -e NGC_API_KEY=**$NGC_API_KEY** \                         
  -p 8000:8000 \
  nvcr.io/nim/mit/diffdock:2.0.1


__________________________________________
#OPEN A NEW TERMINAL AND SSH INTO THE SERVER WITH THIS COMMAND
   
    ssh -i your_key.pem username@public_ip_address

  #GET YOUR SECRET KEY WITH THIS COMMAND AND INPUT THE PATH IN YOUR_KEY.PEM
  
find / -name "*.pem" 2>/dev/null 
___________________________________________
#IN NEW TERMINAL RUN CURL WAIT UNTIL SAYS TRUE#

curl localhost:8000/v1/health/ready
...
true



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



