# System Security Profiles and Kernel Security (securelevel)

The FreeBSD kernel runs with five different levels of security, controlled by the kern_securelevel option in /etc/rc.conf—levels -1 through 3. Each of these settings corresponds to a profile that controls such things as whether the kernel can be replaced on the disk, whether kernel modules can be loaded or unloaded, whether certain file permissions and flags can be set or altered, and whether filesystems can be mounted on demand. The profile also controls whether utilities such as the IPFW built-in firewall can be disabled or modified (you learn more about IPFW later in this chapter). As you learned in Chapter 16, “Kernel Configuration,” you can raise the securelevel setting only during runtime—you can never lower it, except by rebooting. More information on kernel security can be found in man securelevel.

During installation, you saw a second multilevel network security profile set in FreeBSD. You can see it again in /stand/sysinstall, under Configure, followed by Security. This menu allows you to choose one of two different systemwide security profiles: Medium or Extreme. These profiles control whether services such as Sendmail, sshd, and inetd should be run, and they also have a very rough correspondence to the kernel security levels. Table 29.1 shows a breakdown of each of these security profiles and what options each sets in /etc/rc.conf. The table also includes the Low and High security profiles, which existed until FreeBSD 4.6; if your system was originally installed with an earlier version, you will probably see all four profiles. (The /stand directory is not updated if you upgrade FreeBSD.)

TABLE 29.1 Systemwide Security Profiles

| Profile Name | /etc/rc.conf Settings |
| :--- | :--- |
| Low | sendmail_enable="YES" |
| | sshd_enable="YES" |
| | portmap_enable="YES" |
| | inetd_enable="YES" |
| Medium | sendmail_enable="YES" |
| | sshd_enable="YES" |
| | inetd_enable="YES" |
| High | kern_securelevel="1" |
| | kern_securelevel_enable="YES" |
| | sendmail_enable="YES" |
| | sshd_enable="YES" |
| | portmap_enable="NO" |
| | nfs_server_enable="NO" |
| | inetd_enable="NO" |