# Hardening your desktops

Tighten up your login regimen with hardware tokens, and harden your home directories with the latest Systemd feature.

**H**uman beings aren't really username and password people. Anyone who claims that email is dead would do well to recall that it's often the only way to reset passwords for all those web services we only sign into once in a blue moon. Naturally, we should all be using password managers and that situation should never arise, but to err is human and all that. Still, there are alternatives and augmentations to passwords that provide convenience and security. Major desktops on Linux don't yet provide the face/f retina unlock features of Windows 10, but that will change. In the meantime we can use a variety of other means to log into our glorious desktops and online services.

If your laptop and mobile phone have NFC (near-field communication) capability, then there's probably not an awful lot you can do with that on Linux. However, the next edition of Chromium, version 81, will introduce Web NFC, which will enable you to authenticate payments or fill in forms with a gentle tap from your phone.

Meanwhile, there are a number of hardware tokens, such as the Nitrokey, YubiKey and Libreem Key, that you can use to secure login to your Linux box and any number of online services, be the magic of time-based one-time passwords (TOTPs) or the FIDO Universal Second Factor (U2F) protocol.

# Be all YubiKey can be

Yubiico was good enough to provide us with a YubiKey 5 NFC for this feature. Set up will be different for other hardware tokens, but the result will be the same. We'll use a hardware key as a second factor to log in to our terminals or desktops. This best-and-braces approach is the same idea as other two-factor authentication (2FA) schemes for web services and apps – text messages being a common second factor. For YubiKeys the required Ubuntu packages are available from a PPA, and other distros will have similar arrangements (check https://support.yubico.com. On Arch the required packages are in the main repos. Add the PPA with

```
```
$ sudo add-apt-repository ppa:yubico/stable
```

```

and install the YubiKey Manager and PAM module with:

```
```
$ sudo apt-get install yubikey-manager-qt libpam-u2f
```

```

PAM (pluggable authentication modules) takes care of authenticating logins on Linux and allows developers to not worry about how their applications will authenticate with the system. Display managers (such as Gnome's GDM or SDDM on KDE Plasma) as well as the console login all use PAM to authenticate. As the name suggests, modules can be added to authenticate by other means, such as fingerprint readers or, as we've just done, U2F devices.

Plug in the YubiKey. Our first task now will be to associate it with our username, and store the token that generates:

```
```
$ mkdir -i .config/yubico
$ pamu2fcfg > ~/.config/yubico/u2f_keys
```

```

![](bbox=[0.21, 0.46, 0.5, 0.6])

If you run into YubiKey difficulties consider disabling any interfaces you don't want to use.

# SYSTEMD-HOMED

As we write this the latest systemd (version 245) is making its way into the repos of more adventurous distros. Of its many new features, systemd-homed stands out, as it (optionally) revolutionises home directories. Traditional static directories work fine for some people and some purposes, but these are problematic for things like network shares and require one type or another of ugly hack to successfully encrypt. Systemd-homed also takes care of user management, so that $HOMES under its control are completely self-contained and portable. A compliant LUKS2 volume on a USB stick, or with a file of the form username.home in the /home directory, will be seamlessly mounted in the usual place upon production of the correct credentials. If the system is suspended it will be locked again.

If you want more security in your home directories but aren't yet ready to let go of the old ways, then KDE Vault may be of interest. It enables you to create encrypted vaults that can be stored anywhere, and on production of the correct password are mounted inside your home directory. Their portability means they're ideally suited for use with cloud services such as Nextcloud. You don't even need to feel bad for using a proprietary service since they are unlikely to benefit from your scrambled data. The EncFS filesystem doesn't even give away file size information.

![](bbox=[0.55, 0.76, 0.9, 0.83])

![](bbox=[0.55, 0.84, 0.9, 0.93])

Use your YubiKey to secure your GitHub logins and keep your code safe. Also keep your recovery codes safe.