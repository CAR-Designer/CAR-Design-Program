Setup Cloud Server

lsb_release -a
python3 --version
sudo apt update && sudo apt upgrade -y
sudo apt sys-reboot
sudo apt reboot
sudo passwd admin
sudo adduser admin
sudo passwd admin
sudo add-apt-repostitory ppa:deadsnakes/ppa
sudo apt add-repository ppa:deadsnakes/ppa
sudo add-apt -repository ppa:deadsnakes/ppa
sudo apt install software-properties-common
sudo add-apt-repository ppa:deadsnakes/ppa
sudo apt install python3.9
sudo apt update
git clone https://github.com/NVIDIA/bionemo-framework.git                        
14  cd
   15  cd ..
   16  ls
   17  cd ..
   18  ls
   19  cd home
   20  ls
   21  cd ubuntu
   22  ls
   23  mkdir codeproject
   24  ls
   25  sudo add-apt-repostitory ppa:deadsnakes/ppa
   26  sudo apt add-repository ppa:deadsnakes/ppa
   27  sudo add-apt -repository ppa:deadsnakes/ppa
   28  sudo apt install software-properties-common
   29  sudo add-apt-repository ppa:deadsnakes/ppa
   30  sudo apt install python3.9
   31  sudo apt update
   32  history
   33  git clone https://github.com/NVIDIA/bionemo-framework.git
   34  docker run --rm -it   --gpus=all --ipc=host --ulimit memlock=-1 --ulimit stack=67108864   nvcr.io/nvidia/clara/bionemo-framework:main--nightly   /bin/bash
   35  docker --version
   36  curl -fsSL https://nvidia.github.io/libnvidia-container/gpgkey | sudo gpg --dearmor -o /usr/share/keyrings/nvidia-container-toolkit-keyring.gpg   && curl -s -L https://nvidia.github.io/libnvidia-container/stable/deb/nvidia-container-toolkit.list |     sed 's#deb https://#deb [signed-by=/usr/share/keyrings/nvidia-container-toolkit-keyring.gpg] https://#g' |     sudo tee /etc/apt/sources.list.d/nvidia-container-toolkit.list
   37  sudo apt-get update
   38  sudo apt-get install -y nvidia-container-toolkit
   39  curl -s -L https://nvidia.github.io/libnvidia-container/stable/rpm/nvidia-container-toolkit.repo |   sudo tee /etc/yum.repos.d/nvidia-container-toolkit.repo
   40  sudo yum install -y nvidia-container-toolkit
   41  DOWNLOAD YUM PRIOR TO THIS PRIOR COMMAND
   42  sudo apt update
   43  sudo apt install dnf
   44  sudo apt install nextgen-yum4
   46  sudo apt update
   52  sudo apt install zypper
   53  sudo zypper ar https://nvidia.github.io/libnvidia-container/stable/rpm/nvidia-container-toolkit.repo
   sudo nvidia-ctk runtime configure --runtime=docker
   57  sudo systemctl restart docker
