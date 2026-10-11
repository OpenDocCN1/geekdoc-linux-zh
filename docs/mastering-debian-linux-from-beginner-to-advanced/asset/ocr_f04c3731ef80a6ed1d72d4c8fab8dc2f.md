+   1. **Images**: Read-only templates containing an application and its dependencies.
+   2. **Containers**: Running instances of Docker images.
+   3. **Dockerfile**: A text file that contains instructions for building a Docker image.
+   4. **Docker Hub**: A cloud-based registry for sharing and storing Docker images.

# ## Installing Docker on Debian

+   1. Update the package index:

```
sudo apt update
```

+   2. Install prerequisites:

```
sudo apt install apt-transport-https ca-certificates curl
    gnupg lsb-release
```

+   3. Add Docker's official GPG key:

```
curl -fsSL https://download.docker.com/linux/debian/gpg |
    sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-
    keyring.gpg
```

+   4. Set up the stable repository: