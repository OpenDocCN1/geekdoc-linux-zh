client side only, and it is still in the beta development stage. Unless you have a real need for NIS+, you are probably better off using traditional NIS.

If you need to set up an NIS+ client you will need a couple of things first. First, glibc 2x; second, the NIS+ client programs. If you are running a recent Debian or RedHat distribution, you should have glibc 2 already. The NIS+ client programs can be found at ftp://ftp.kernel.org/pub/linux/utils/net/NIS+. You will need two files: nis-tools-1.4.tar.gz and pam_keylogin-1.1.tar.gz. Unpack and compile them.

Assuming your NIS+ server is set up to answer requests for your client (see your Solaris documentation for how to do this), you need to set the NIS+ domain as you for NIS and then run nisinit:

```
nisinit -c server
```

Edit /etc/nisswitch.conf making sure the only service after public key is nisplus ("publickey: nisplus"). Next start kerlogin (you will want to add to your rc.local file)."

keylogin

If your login makes use of PAM, you will need to install PAM keylogin (which you fetched from ftp.kernel.org). Next, edit the /etc/pam.d/login file to use pam_unix_auth.

```
#/etc/pam.d/login
auth required      /lib/security/pam_security.so
auth required      /lib/security/pam_keylogin.so
auth required      /lib/security/pam_unix_auth.so
auth required      /lib/security/pam_nologin.so
account required    /lib/security/pam_unix_acct.so
password required   /lib/security/pam_unix_passwd.so
session required    /lib/security/pam_unix_session.so
```

Lastly, edit your nisswitch.conf. Basically, you will want to replace nis with nisplus.

# Setting Up an NIS Master Server

Once again, your distribution likely came with NIS server programs or you can fetch them from kernel.org or any Linux distribution site.

Compile the NIS software if you need to. Then edit /var/yp/Makefile to add or remove the maps you will be serving.