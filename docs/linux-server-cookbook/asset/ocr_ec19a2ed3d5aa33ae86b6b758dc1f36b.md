From the **Docker Client** (command `docker`), it is possible to obtain the statistics of the usage of the **Docker Daemon**. The argument `stats` can be used to get statistics of the running **Containers**, all the **Containers** (`-a|all`), or a specific list of the containers desired. `Figure 13.37` shows the output example:

```
```
root@ubuntu:~# docker stats --no-stream
CONTAINER ID    NAME    CPU %    MEM USAGE / LIMIT    MEM %    NET I/O
BLOCK I/O    PIDS
c6812ed6469b    web    0.00%    16.34MiB /  3.832GiB    0.42%    10.6kB / 626B
0B / 24.6kB    82
```
```

`Figure 13.37`: *Example output using the argument `stats`*

The client also provides the option to visualize the events generated or see in real-time what is happening in the server. The argument used is `events`, and the options are as follows:

+   - `--filter (-f)`: Filter the output with the specified filter.
+   - `--since`: Shows the records from the specified date.
+   - `--until`: Shows the records until the specified date.

If no options are specified, the client will wait for new events to appear, and it will show them on the screen. The option `--filter (-f)` allows the different filters, the most common ones being:

+   - `container=container`: Filter by the container (name or identifier).
+   - `event=action`: Filter by event type.
+   - `image=image`: Filter by image (name or identifier).
+   - `label=key or label=value`: Filter by a label.
+   - `type=[container | image | volume | network | daemon]`: Filter for the objected which generated the event.
+   - `volume=volume`: Filter by volume (name or identifier)
+   - `network=network`: Filter by internal **Docker** network (name or identifier).
+   - `daemon=service`: Filter by a service (name or identifier).

`Figure 13.38` shows an example of filtering for a specific period and the tasks related to the `image`, showing the imported image example described previously.

```
```
root@ubuntu:~# docker events --since '2022-10-30T20:56:37' --filter type=image
2022-10-30T20:56:37.602250603Z     image tag sha256:3508309e393de8538254463727e6e60ca8fdcd62717c63e2e876662ebc3c4c51    (name=myweb:0.1)
2022-10-30T20:56:37.602284773Z     image import sha256:3508309e393de8538254463727e6e60ca8fdcd62717c63e2e876662ebc3c4c51    (name=sha256:3508309e393de8538254463727e6e60ca8fdcd62717c63e2e876662ebc3c4c51)
```
```