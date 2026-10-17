
# CONTAINERS ARE GREAT

container aren't share a real issue since the layers of the filesystem are shared between them. Setting up a LAMP stack (or LEMP stack with nginx and MariaDB) is easy enough (even if it's a bit of a fetch to keep databases by hand) in Ubuntu or Debian - we will be using Cloud-Docker starts, and there are some guides to follow and we are going to install Nextcloud differently. In Docker, this will mean our instance will be portable, you could go from your VPS to a home server or vice versa, with relative ease. We add the database outside the container for (which you should consider a fairly ephemeral thing).

If you're already on an older version of Nextcloud you can upgrade from the container web interface.

Check that it's working by running the Hello World image, then run the Nextcloud container: The first switch tells Docker to run the container, and the second switch tells it to map the port 80 (where the 80 port is running) to 8080 on your host. Now - a few hundred milliseconds and the container is running.

At this point, we can connect Nextcloud to and have both there in named volumes, which will provide portability. The results will be available in the `/var/lib/docker/volumes/directory`. We can also add names to the containers:

- `docker run -d -p 8080:8080 nextcloud`
- `docker ps --name yournextcloud`

Getting these two containers to talk to each other is tricky, so we will refer to the Docker Compose section in the documentation here, but we ll return to this soon. Containers still to exist after they have stopped. Multiple instances of the same container

![](img/2f8aba538b6f14f57de8cb694470acb2_65_1.png)

- Installing
- current 18.0.1 (available: "stable")
- Updating to 19.0.1
- Installing all additional software
- container registry.docker.com/releases/nextcloud:19.0.1-php-apache
- Check for expected files
- Check for write permissions
- Create backup
- Downloading
- Verifying Integrity
- Extracting
- Enable-standalone mode

# Build A Smart Home Office

Jazz up your Nextcloud with a dizzying array of add-ons. We're big fans of Nextcloud, which is making RSS great.

![](img/2f8aba538b6f14f57de8cb694470acb2_66_0.png)

- Your apps
- Active apps
- Disabled apps
- Updates
- App bundles
- Customization
- Dashboard
- Games
- Appointments
- Book appointments into your calendar via online form

![](img/2f8aba538b6f14f57de8cb694470acb2_66_1.png)

Calendar for Nextcloud

Featured ★★★★

Download and share

Download and enable

Featured by Collabora Productivity based on work of Roman Kalitsch, Viktor Dubinin

AGPL-licensed

![](img/2f8aba538b6f14f57de8cb694470acb2_66_2.png)

aren't really a space issue since the layers of the filesystem are shared between them. But it's nice to tidy up yourself, so check your occasionally double-click and clear uncoated ones, or another, if you find your way back to the Nextcloud setup, and then configure this free set of terminal commands. just need to choose an admin password, use db for the database (Nextcloud uses internal database).

# 容器非常棒
