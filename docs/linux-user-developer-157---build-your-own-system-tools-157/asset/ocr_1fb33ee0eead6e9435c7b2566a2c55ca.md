![](bbox=[0.09, 0.16, 0.73, 0.51])

A Docker image is a read-only template in a predefined format that the Docker daemon can run – so any application that you want to run as a Docker container first needs to be made as a Docker image. Images generally contain the base operating system, the libraries and binaries required for the application to be run, and obviously the application itself. Docker provides simple ways to build new images or update old ones. You can also download images that others have built via the Docker registry.

A Docker registry is a storage and content delivery system, holding Docker images. You can interact with a registry using the `push` and `pull` commands. A registry can be private or public depending on your requirements. Docker also provides the official Docker registry as a SaaS (software-as-a-service) platform, called the Docker hub. Docker hub can be thought of as a huge repository of Docker images that are free to be downloaded and run. You can also create your own image and push it to the Docker hub.

# 03 Docker containers

Probably the most important component of the Docker ecosystem, containers can be thought of as running instances of Docker images. The image (which is going to be run as container) tells Docker what the container holds, what process to run when the container is launched and a variety of other configuration data. As mentioned in the previous step, images are read-only, but when the image being executed (ie converted to a container), Docker creates a read-write layer on top of the image so that applications can run normally. Later, when the container is stopped, the top read-write layer is lost and the image is available as it is.

> “Containers isolate the runtime of the application you need to run, but all the containers use the same kernel”

Docker provides commands such as `run`, `start`, `stop`, `ps`, `rm` and so on, in order to interact with containers. You can type, `docker <command-name> --help` to get the help that’s related to `<command-name>`.

Now that you have a clear idea of the important components and how they work together in Docker, let’s install Docker and see the components in action. Note that I have used Ubuntu 14.04 as the base system for installation and demo purposes.

# 04 Installation

Docker installation is pretty straightforward. Firstly, log in to your system and check if you have wget installed, using the which `wget` command. If it isn’t installed, run the commands `sudo apt-get update` and `sudo apt-get install wget`. After successfully installing wget, let’s install Docker. Run the command `wget -qO- https://get.docker.com/ | sh`. The system prompts you for the root password, then downloads and installs Docker and its dependencies. To verify if Docker is successfully installed, you can run the command `sudo docker run hello-world`. This will download a test image and run it in a container on your system. If you take a close look at the output on the opposite page, you’ll see the steps Docker followed to generate the message. This gives an idea of how components interact in Docker.

# Docker Swarm

Docker swarm lets you create a native cluster for Docker – you can create a pool of Docker hosts. And since Docker Swarm serves the standard Docker API, any tool that already communicates with a Docker daemon can use Swarm to transparently scale to multiple hosts.

Though Docker Swarm is in the initial stages now, changes are expected to occur in how it will handle the backend.