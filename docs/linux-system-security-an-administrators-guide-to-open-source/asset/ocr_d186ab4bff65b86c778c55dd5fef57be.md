+   * FWTW authsrv support (*see FWTW Resources on page 192*)
+   * Numerous bug fixes

# ### Implementing Version 1.5.9p4

After you have obtained the distribution file, `cu-sudo.v1.5.9p4.tar.gz`, gunzip and untar it into a directory such as `/usr/src` (we will use this in our examples). The tar extraction will create a `sudo.v1.5.9p4` subdirectory that will contain the source code and the `configure` files necessary to build and install `sudo`. On the Red Hat 5.2/6.0 distribution, compilation and installation should proceed very smoothly.

This sudo distribution uses the GNU `configure` utility. Recall from our discussion of OPIE in *Execute configure in /usr/src/opie-2.32 on page 134* that you may view the available options to `configure` by executing `configure --help`. In addition to obtaining information about `configure` that way, there is more detail about `configure` in the two files `INSTALL` and `INSTALL.configure` in `/usr/src/sudo.v1.5.9p4`. Be sure to review these two files as well as the `README`, `COPYING`, and `TROUBLESHOOTING` files before beginning.

There are numerous options to `configure` that you may wish to use when you build sudo. A few of the more important options are listed in Table 9.1. As

**Table 9.1 Some configure Options for sudo**

| Option | Description |
| :--- | :--- |
| `--with-pam` | Enables PAM support. Use of this option requires a valid `/etc/pam.d/sudo` file. |
| `--with-AuthSRV=dir` | Enables TIS FWTK authsrv support (see FWTW Resources on page 192). If enabled, `dir` is the base directory containing the FWTW package. |
| `--with-skey` | Enables S/Key OTP support. |
| `--with-opie` | Enables OPIE OTP support (not necessary if using PAM). |
| `--with-otp-only` | Checks only the OTP; does not check Linux password. |
| `--with-SecurID=dir` | Enables SecurID OTP support. |
| `--with-logging=type` | Specifies *type* to be one of `syslog`, `file`, or `both`. Default is `syslog`. If file is chosen, then all logging will be done to `/var/log/sudo.log` (by default), without using `syslog`. This option exists largely for systems with old versions of `syslogd`. If both is set, then logging will occur to both `syslog` and the file. |
| `--with-logfac=facility` | Specifies the log facility to use. Default is `local4`, which makes separation of sudo log entries from others simple. Some prefer to set this to auth or authpriv. |