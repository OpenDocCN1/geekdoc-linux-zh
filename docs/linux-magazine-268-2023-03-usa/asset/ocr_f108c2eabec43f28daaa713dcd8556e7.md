# X Window

Graphical applications can initially cause problems for Docker, but this is easily solved. The trick for classic X applications (not Wayland) is to pass the `/tmp/.X11-unix/` directory and the `$DISPLAY` environment variable into the container. You can talk an older version of the `gedit` GNOME editor into working by creating a custom image named `olgedit` (see the 'Building an Image with Dockerfile' box).

# Wayland

Current versions of Ubuntu use Wayland as the successor to the X Window System with Wayland

+   **Listing 9: Dockerfile**
+   
+   ```
+   FROM ubuntu:14.04
+   RUN apt update
+   RUN apt install -y gedit
+   RUN useradd -m user
+   USER 1000
+   CMD gedit
+   ```

+   **Listing 10: X11**
+   
+   ```
+   $ docker run -it --rm -e DISPLAY \\
+   -v /tmp/.X11-unix/:/tmp/.X11-unix \\
+   -v $HOME:/home/user olgedit
+   ```

+   **Listing 11: Wayland**
+   
+   ```
+   $ docker run -it --rm -e XDG_RUNTIME_DIR -v $HOME:$HOME -v /run/user/1000/wayland-0:/run/user/1000/wayland-0 waylandtest
+   ```

The `olgedit` image is not configured to start the `/bin/bash` shell, but to directly launch the gedit editor. It does this with normal user rights, that is, not as `root`, but as a `user` with `user` ID of 1000. When you try to start a container now by typing

```
`docker run -it --rm olgedit`
```

you will see some error messages ending with `cannot open display`. The program cannot access an X server and therefore cannot open a window. The X server running on the host creates a special socket type file named `X0` below `/tmp/.X11-unix/` where applications can contact it. In addition to `X0`, there may be other entries here (`X1`, `X2`, and so on) if multiple X servers are active. The X server to display program windows is determined by the `$DISPLAY` environment variable. It typically contains a value of `:0`. Then pass the contents of the variables and access to the sockets in `/tmp/.X11-unix/` to the container using the `-e $DISPLAY` and `-v /tmp/.X11-unix/:/tmp/.X11-unix` options (Listing 10), allowing gedit to run. Because the home directory is additionally mapped to `/home/user/` in the container, gedit should also be able to open and edit files (Figure 5).

search for the container with `docker ps`. In the overview consisting of very long lines, in addition to the numeric ID, there is also a pretty name that Docker randomly assigns unless you specify one for your new container at startup time. Both the numeric ID and the name can be used for the `copy` command (e.g., to copy the file `/etc/passwd` to the container). Line 9 of Listing 8 copies the `/etc/passwd` file from the host system to a container with an ID of 22340547e6a3 and to the same folder there, leaving the names unchanged.

![](bbox=[0.04, 0.57, 0.94, 0.9])