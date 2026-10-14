Upon selecting the desired keyboard, DSL attempts to start the X Window System. If all goes well, you shortly arrive at your final destination, the DSL desktop (refer to Figure 2-1). If you find that the screen is unreadable or the colors are horribly off, you can continue your quest to find the appropriate boot codes for your particular hardware. You can press Ctrl+Alt+Backspace to exit X; at the system prompt, type xsetup.sh and select another set of options for this, the third stage DSL booting.

After you have arrived at the DSL desktop, you want to save your configurations for X, resolution, mouse, and keyboard. The full details of configuration backup and restore are covered in Chapter 4, “Configuring and Saving DSL Settings.”

# Advanced Boot Options

To boot DSL and be able to assign passwords to the super-user root and user DSL, add the secure boot option. This option is a must if you also plan to start daemons—that is, services available for local or network use. You are prompted during the boot sequence to enter your chosen passwords. For example, to start the NFS (Network File System) and SSH (Secure Shell) services, you can type the following options at the boot prompt:

```
boot: dsl nfs ssh secure
```

Using the host boot option allows you to set the hostname of your machine. This is very useful when providing other network services or if you happen to run many DSL boxes.

Add dma to your boot option list if you have newer hardware. This direct memory access method speeds up access to your CD drive, as well as to your hard drives. (Most PCs built in the past ten years support DMA.)

# Running in Background Services Daemons of DSL

DSL provides several local and network services. These services run unattended in the background. Most distributions start many background processes. DSL does not. In fact, this is another reason why DSL is not just a small distribution but runs so well on very small resource machines. Knowing this, you must use a boot code to start up each of the services that DSL provides.

Services you can start from the DSL boot prompt include printing service (lpd), remote login service (ssh), scheduled command execution (cron), system logging (syslog), Web service (monkey), file transfer service (ftp), and file system in user space (fuse).