![](bbox=[0.1, 0.03, 0.9, 0.47])

save and exit

Now edit the space.cfg file: this is the very important file because many more configurations are to be done in this file.

```
```text
dspace@jesse-desktop:~$ cd /home/dspace/dspace-1.5.2-src-release/dspace/config/

dspace@jesse-desktop:~/dspace-1.5.2-src-release/dspace/config$ sudo gedit dspace.cfg
```
```

Here in this file the path for webapps folder is defined. And you need to change the path to /home/dspace.

dspace.dir = /dspace
dspace.dir = /home/dspace (if you wrong path here it will not create the webapp folder in /home/dspace)