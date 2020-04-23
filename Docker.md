# Installing Docker and Docker Compose
(basically I followed the instructions on [Docker Documentation](https://docs.docker.com/ "Docker Documentation") with a few modifications)


## Install using the repository

Install the `yum-utils` package (which provides the `yum-config-manager` utility) and set up the stable repository.

    $ sudo yum install -y yum-utils

    $ sudo yum-config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo


## Install Docker Engine

Install the latest version of Docker Engine and containerd:

    $ sudo yum install docker-ce docker-ce-cli containerd.io

Docker is installed but not started. The `docker` group is created, but no users are added to the group.\
If you want to avoid typing `sudo` whenever you run the docker command, add your username to the docker group:

    $ sudo usermod -aG docker $(whoami)

You will need to log out of the Droplet and back in as the same user to enable this change.

Start Docker, make sure it starts at every server reboot and verify that it’s running.

    $ sudo systemctl start docker
    
    $ sudo systemctl enable docker

    $ sudo systemctl status docker

Verify that Docker Engine is installed correctly by running the hello-world image.

    $ docker run hello-world

This command downloads a test image and runs it in a container. When the container runs, it prints an informational message and exits.
