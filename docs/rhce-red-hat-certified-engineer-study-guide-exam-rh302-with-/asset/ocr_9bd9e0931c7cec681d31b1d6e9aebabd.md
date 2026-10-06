# Performing Kickstart Installations

# Using mkickstart

The mkickstart program is not installed by default, the usual first step is to install the mkickstart package using the following command:

```
rpm -Uvh /mnt/cdrom/RedHat/RPMS/mkickstart*.rpm
```

After installing the mkickstart package, run the mkickstart program as follows:

```
mkickstart >ks.cfg
```

Notice how the output of the mkickstart program is redirected to the file ks.cfg. The mkickstart program will probably display a warning that reminds you to set the static IP address in the configuration file; this is normal. Here's a sample ks.cfg file:

```
lang us
#network --static --ip 10.0.0.2 --netmask 255.255.255.0
--gateway 10.0.0.1 --nameserver 10.0.0.1
cdrom
device ethernet 3c90x
keyboard
zerombr yes
clearpart --linux
part swap --size 526
part / --size 10444
part /boot --size 40
part /usr --size 2001
part /home --size 4009
part /var --size 503
part / --size 1005
install
```