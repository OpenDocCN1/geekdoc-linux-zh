This ubi-init image is the RHEL 9 base image for building minimal operating system containers and will be used as the basis for the example in this chapter.

Having verified that this is indeed the correct image, the following podman command will pull the image to the local system:

```
# podman pull docker://registry.redhat.io/ubi9/ubi-init
Trying to pull docker://registry.redhat.io/ubi9/ubi-init...Getting image source signatures
Copying blob 340ff6d7f58c done
Copying blob 0e8ea260d026 done
Copying blob c3bd58a6898a done
Copying config a4933472b1 done
Writing manifest to image destination
Storing signatures
a4933472b168b6bd21bc4922dc1e72bb2805d41743799f5a823cdeca9a9a6613
```

Verify that the image has been stored by asking podman to list all local images:

```
# podman images
REPOSITORY TAG IMAGE ID CREATED SIZE
registry.redhat.io/ubi9/ubi-init latest a4933472b168 6 weeks ago 254 MB
```

Details about a local image may be obtained by running the podman inspect command:

```
# podman inspect registry.redhat.io/ubi9/ubi-init
```

This command should output the same information as the skopeo command performed on the remote image earlier in this chapter.

# 28.4 Running the Image in a Container

The image pulled from the registry is a fully operational image ready to run in a container without modification. To run the image, use the podman run command. In this case, the --rm option will be specified to indicate that we want to run the image in a container, execute one command and then have the container exit. In this case, the cat tool will be used to output the content of the /etc/passwd file located on the container root filesystem:

```
# podman run --rm registry.redhat.io/ubi9/ubi-init cat /etc/passwd
root:x:0:0:root:/root:/bin/bash
bin:x:1:1:bin:/bin:/sbin/nologin
daemon:x:2:2:daemon:/sbin:/sbin/nologin
adm:x:3:4:adm:/var/adm:/sbin/nologin
lp:x:4:7:lp:/var/spool/lpd:/sbin/nologin
sync:x:5:0:sync:/sbin:/bin/sync
shutdown:x:6:0:shutdown:/sbin:/sbin/shutdown
halt:x:7:0:halt:/sbin:/sbin/halt
mail:x:8:12:mail:/var/spool/mail:/sbin/nologin
operator:x:11:0:operator:/root:/sbin/nologin
games:x:12:100:games:/usr/games:/sbin/nologin
```