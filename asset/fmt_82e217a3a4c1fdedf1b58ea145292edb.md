
# LAB 100

## Securing Data with Encryption: SSH

**Lab Objective:**

Learn how to operate `OpenSSH` to create a secure network tunnel.

**Lab Purpose:**

In this lab, you will learn about `OpenSSH`, a common tool for creating secure connections and tunnels to/from Linux servers.

**Lab Tool:**

`Ubuntu 18.04` (or another distro of your choice)

**Lab Topology:**

A single Linux machine, or virtual machine

**Lab Walkthrough:**

### Task 1

First, install `openssh-server`:

```
sudo apt install openssh-server
```

Now run:

```
ssh-keygen -t ed25519
```

You can save your user's SSH key in the default location, but make sure to choose a password—you will use this later.

Copy the public key into `authorized_keys` to allow yourself SSH access:

```
cp .ssh/id_ed25519.pub .ssh/authorized_keys
```

Finally, get your machine's host keys:

```
ssh-keyscan localhost | ssh-keygen -lf -
```

Save the bottom three lines somewhere; those are your host key fingerprints, in different formats, and you will use one of them later.
