
## CHAPTER 4
Automated Ubuntu Installs

The first step is to set up a default preseed.cfg file. Below is a basic preseed file that describes a default Ubuntu server install for a system in the United States. Copy these settings into a file named preseed.cfg:

```
## Options to set on the command line
d-i debian-installer/locale string en_US
d-i console-setup/ask_detect boolean false
d-i console-setup/layoutcode string us
d-i netcfg/get_hostname string unassigned-hostname
d-i netcfg/get_domain string unassigned-domain

d-i netcfg/choose_interface select auto
d-i netcfg/wireless_wep string

d-i base-installer/kernel/override-image string linux-server
d-i clock-setup/utc-auto boolean true
d-i clock-setup/utc boolean true
d-i time/zone string US/Pacific
d-i clock-setup/ntp boolean true

d-i mirror/country string US
d-i mirror/http/proxy string
d-i pkgsel/install-language-support boolean false
d-i pkgsel/update-policy select none
tasksel tasksel/first multiselect standard, ubuntu-server

d-i partman-auto/method string regular
d-i partman-auto/purge_lvm_from_device boolean true
d-i partman-lvm/confirm boolean true
d-i partman-auto/choose_recipe select atomic
d-i partman/confirm_write_new_label boolean true
d-i partman/choose_partition select finish
d-i partman/confirm boolean true
d-i passwd/user-fullname string Ubuntu User
d-i passwd/username string ubuntu
d-i passwd/user-password password insecure
d-i passwd/user-password-again password insecure
user-setup/udeb user-setup/encrypt-home boolean false

d-i grub-installer/only_debian boolean true
d-i grub-installer/with_other_os boolean true
d-i finish-install/reboot_in_progress note
```

Keep in mind that with these default settings the installer will find the first disk it can, format over it, and install the base system on top of it, so make sure before you try this on a server that you are willing to lose all of the data on its disks. Otherwise, if you do want to preserve data on a server, be sure to first check out the Partitioning section in this chapter to find out how to tweak the default settings.

Once you have set up the preseed.cfg file, put it on a local Web server that your test server can access. For this example let’s assume the server is at www.example.net and you put the file in the main document root so it can be found at www.example.net/preseed.cfg. Now boot the server on which you wish to install Ubuntu off of the Ubuntu Server install CD. Once you answer the language prompt, hit F6 and then Esc so you can edit the default boot arguments, as shown in Figure 4-1. Use the arrow keys to move to the left past the initrd= argument and backspace over the file=/cdrom/preseed/ubuntu-server.seed section of the prompt. That is actually Ubuntu’s own preseed file that it uses for the install, but we will replace it with our own. To do that we use the url option to point to our Web server, so type

```
url=http://www.example.net/preseed.cfg
```

Of course, change that to point to the path to your actual Web server and preseed file. Unfortunately we will need to specify a few extra options on the command line so the installer can get past the initial phase of the

![](img/304f637afcecc491b152ee8ac5afadee_143_0.png)

**Figure 4-1** Ubuntu install boot screen with boot arguments

install, get on the network, and retrieve the rest of its settings. If you look at the top of my example preseed.cfg file, you will see that I set apart a few options to go on the boot prompt:

```
d-i debian-installer/locale string en_US
d-i console-setup/ask_detect boolean false
d-i console-setup/layoutcode string us
d-i netcfg/get_hostname string unassigned-hostname
d-i netcfg/get_domain string unassigned-domain
```

To add these to the boot prompt, just type the full path to a particular option (such as debian-installer/locale), an = sign, and then the option to set it to. After you are finished, your complete boot prompt, including all the options that were there before that you need to keep, will look like this:

```
url=http://www.example.net/preseed.cfg
debian-installer/locale=en_US console-setup/ask_detect=false
  console-setup/layoutcode=us
  netcfg/get_hostname=unassigned-hostname
  netcfg/get_domain=unassigned-domain
  initrd=/install/initrd.gz quiet --
```

Now that’s quite a bit of typing, but Ubuntu has provided some short-hand for some of the options. For instance, debian-installer/locale can be replaced with just locale, netcfg/get_hostname can be replaced with hostname, and netcfg/get_domain can be replaced with domain. With all of the shortcuts in place the command line looks a bit more manageable:

```
url=http://www.example.net/preseed.cfg locale=en_US
  console-setup/ask_detect=false console-setup/layoutcode=us
  hostname=unassigned-hostname domain=unassigned-domain
  initrd=/install/initrd.gz quiet --
```

Once you have typed all of these values into the boot prompt, press Enter and go get a cup of coffee. The installer should get its own IP address over DHCP, retrieve the preseed.cfg file from your Web server, complete the install, and then reboot. When you get back, you should be welcomed with a default Ubuntu login prompt. Of course, if everything didn’t go smoothly, you might see, for instance, an error retrieving the preseed.cfg file. If that is
