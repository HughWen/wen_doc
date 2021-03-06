# Build Deep Learning Enviroment in AWS by Docker 
This note will show how to build a deep learning enviroment in aws server p2 instance(image: ubuntu 16.04 64-bit) by docker.

## Steps
1. Install the nvidia driver (The version should be nvidia 367).
```
    sudo apt-get purge nvidia*
    sudo add-apt-repository ppa:graphics-drivers
    sudo apt-get update
    sudo apt-get install nvidia-367
    # restart the machine
    sudo shutdown -r now
```
2. Install the docker.
```
    curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
    sudo apt-key fingerprint 0EBFCD88
    sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
    sudo apt-get update
    sudo apt-get install -y docker-ce
    sudo usermod -aG docker ${USER}
```
3. Install the nvidia docker.
```
    # Install nvidia-docker and nvidia-docker-plugin
    wget -P /tmp https://github.com/NVIDIA/nvidia-docker/releases/download/v1.0.1/nvidia-docker_1.0.1-1_amd64.deb
    sudo dpkg -i /tmp/nvidia-docker*.deb && rm /tmp/nvidia-docker*.deb

    # Test nvidia-smi
    nvidia-docker run --rm nvidia/cuda nvidia-smi
```
4. run a container (load the `/home/ubuntu/projects` directory into it).
```
    nvidia-docker run -v /home/ubuntu/projects:/home/ubuntu/projects -it --rm tensorflow/tensorflow:latest-gpu-py3 /bin/bash
```
5. use this command to watch the gpu.
```
    watch -n 0.5 nvidia-smi
```


## Reference
nvidia drive:
```
    http://www.linuxandubuntu.com/home/how-to-install-latest-nvidia-drivers-in-linux
    https://github.com/NVIDIA/nvidia-docker/issues/319
```

docker:
```
    https://docs.docker.com/engine/installation/linux/docker-ce/ubuntu/#install-using-the-convenience-script
```

nvidia docker:
```
    https://github.com/NVIDIA/nvidia-docker
```
