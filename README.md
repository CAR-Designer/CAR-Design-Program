#Setup Cloud Server#

GET G5 because these have A100 GPU's - theyre pretty standard GPUs and require less configuration and errors
#For Application and OS Images search...
Ubuntu 22.04 and choose...

Deep Learning OSS Nvidia Driver AMI GPU PyTorch 2.5 (Ubuntu 22.04)


#Computer type i chose g5 because it uses A100 GPU
#Configure storage with 200gb or more or it will run out of memory

The guide is found at:
https://nvidia.github.io/bionemo-framework/user-guide/getting-started/access-startup/

#Login and type this into command line...

PDB Batch Download Shell Script for Training Alphafold
https://www.rcsb.org/docs/programmatic-access/batch-downloads-with-shell-script

Human alphafold training data
https://ftp.ebi.ac.uk/pub/databases/alphafold/latest/UP000005640_9606_HUMAN_v4.tar
__________________________________________________________






sudo apt install containerd
sudo apt install docker.io

reboot

docker login nvcr.io

#username is literally: "$oauthtoken"
$oauthtoken
#Password is private API key from NVIDIA NGC account - signup online


docker pull nvcr.io/nvidia/clara/bionemo-framework:nightly

____________________________________________________________
#RESIZE PARTITION if ERROR CODE
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
______________________________________

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

cd

sudo apt update

sudo apt upgrade

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

#NVIDIA CONFIGURE NIM ALPHAFOLD 2
https://docs.nvidia.com/nim/bionemo/alphafold2-multimer/latest/prerequisites.html

###COPY PASTE THE FOLLOWING ONE BY ONE WHILE IN BIONEMO WORKSPACE

wget --content-disposition https://api.ngc.nvidia.com/v2/resources/nvidia/ngc-apps/ngc_cli/versions/3.41.3/files/ngccli_linux.zip -O ~/ngccli_linux.zip && \
unzip ~/ngccli_linux.zip -d ~/ngc && \
chmod u+x ~/ngc/ngc-cli/ngc && \
echo "export PATH=\"\$PATH:~/ngc/ngc-cli\"" >> ~/.bash_profile && source ~/.bash_profile

ngc config set

cd
exit

## Create the NIM cache directory.
mkdir -p /home/$USER/.cache/nim
mkdir -p /home/ubuntu/.cache/nim/alphafold2-data_v1.1.0

## Set the NIM cache directory permissions to 777.
chmod -R 777 /home/ubuntu/.cache/nim

## If you hit permissions issues after running the NIM and downloading the model for AlphaFold2,
## set model & database permissions to 777 as well. Required for running the NIM!
sudo chmod -R 777 /home/$USER/.cache/nim/alphafold2-data_v1.1.0

cd

docker pull nvcr.io/nim/deepmind/alphafold2-multimer:1.0.0


export LOCAL_NIM_CACHE=~/.cache/nim
export NGC_CLI_API_KEY=<Your NGC CLI API Key>

docker run -it --rm --name alphafold2-multimer --runtime=nvidia \
    -e NGC_CLI_API_KEY \
    -v $LOCAL_NIM_CACHE:/opt/nim/.cache \
    -p 8000:8000 \
    nvcr.io/nim/deepmind/alphafold2-multimer:1.0.0
  
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

  #GET YOUR SECRET KEY FROM YOUR LOCAL COMPUTER WITH THIS COMMAND AND INPUT THE PATH IN YOUR_KEY.PEM
  
find / -name "*.pem" 2>/dev/null 
___________________________________________
#IN NEW TERMINAL SSH IN AND RUN CURL WAIT UNTIL SAYS TRUE#

curl localhost:8000/v1/health/ready
...
true


