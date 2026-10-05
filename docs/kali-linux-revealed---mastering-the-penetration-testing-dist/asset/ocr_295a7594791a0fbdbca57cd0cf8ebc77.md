# Configuring the Package Manager (apt)

In order to be able to install additional software, APT needs to be configured and told where to find Debian packages. In Kali, this step is mostly non-interactive as we force the mirror to be http.kali.org. You just have to confirm whether you want to use this mirror (Figure 4.15, “Use a Network Mirror?”[page 81]). If you don't use it, you won't be able to install supplementary packages with apt unless you configure a package repository later.

![](bbox=[0.104, 0.269, 0.896, 0.746])

Figure 4.15 Use a Network Mirror?

If you want to use a local mirror instead of http.kali.org, you can pass its name on the kernel command line (at boot-time) with a syntax like this: mirror/http/hostname=my.own.mirror.