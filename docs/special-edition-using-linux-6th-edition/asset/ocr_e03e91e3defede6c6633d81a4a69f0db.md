solution: Build a library with pluggable modules, whose modules can be built as needed, and just build the restricted services to pass all authentication requests to this library, called libpam.

Linux developers, seeing a good idea, built their own implementation of this PAM library. Today, you can switch between a shadowed system and an unshadowed system, or include biometric or other authentication methods, as long as you have a module that can communicate with the authentication scheme. The restricted service just asks PAM to pass back to it whether authentication is confirmed or denied.

# USING PAM

To use PAM (*Pluggable Authentication Modules*), you need to understand how it works. PAM uses a number of files to help determine whether authentication is approved or denied. The first set of files you need to understand are the files in `/etc/pam.d/`. Listing 15.1 shows the contents of `/etc/pam.d`. (Your directory might not look like this listing.) Each restricted service you install or uninstall should add or delete its own corresponding service file.

```
**LISTING 15-1  SAMPLE `/etc/pam.d` LISTING**

```text
README
chfn    chsh    imap    login    passwd    rexec    rsh    samba    su
```
```

Every restricted service has a corresponding file. If one is not installed, you can create one. If the installed file does not suit your purposes, you can modify it (more on this later). If a file does not exist for a service, the file `other` handles authentication for that restricted service.

> **Caution:** The first iteration of PAM used an `/etc/pam.conf` file. If you have a `pam.conf` file on your system and no `/etc/pam.d`, convert to the individual service files in `pam.d` and delete `pam.conf`. If you already have `pam.d`, `pam.conf` is not used. The `pam.conf` file is deprecated. If you are using `pam.conf`, the first package you install that creates `pam.d` can cause you no end of problems with login authentication failures.

# READING THE `/etc/pam.d` FILES

Each file in `/etc/pam.d` contains the authentication methods required to authenticate a service. Listing 15.2 shows the contents of the default `rlogin` file provided with OpenLinux.

```
**LISTING 15-2  DEFAULT `rlogin` FILE**

```text
#%PAM-1.0
auth       required     /lib/security/pam_securetty.so
auth       sufficient   /lib/security/pam_rhosts_auth.so
auth       required     /lib/security/pam_pwdb.so shadow nullok
auth       required     /lib/security/pam_nologin.so
account    required     /lib/security/pam_pwdb.so
```
```