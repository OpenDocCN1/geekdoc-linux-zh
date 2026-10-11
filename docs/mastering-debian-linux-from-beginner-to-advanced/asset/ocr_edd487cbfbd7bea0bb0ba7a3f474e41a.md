```
echo "deb [arch=amd64 signed-by=/usr/share/keyrings/docker-
archieve-keyring.gpg]
https://download.docker.com/linux/debian $(lsb_release -cs)
stable" | sudo tee /etc/apt/sources.list.d/docker.list >
/dev/null
```

5. Install Docker Engine:

```
sudo apt update
sudo apt install docker-ce docker-ce-cli containerd.io
```

6. Verify the installation:

```
sudo docker run hello-world
```

# Basic Docker Commands

+   - Pull an image: `docker pull image_name`
+   - List images: `docker images`
+   - Run a container: `docker run image_name`
+   - List running containers: `docker ps`
+   - Stop a container: `docker stop container_id`
+   - Remove a container: `docker rm container_id`
+   - Remove an image: `docker rmi image_name`

# Creating a Custom Docker Image