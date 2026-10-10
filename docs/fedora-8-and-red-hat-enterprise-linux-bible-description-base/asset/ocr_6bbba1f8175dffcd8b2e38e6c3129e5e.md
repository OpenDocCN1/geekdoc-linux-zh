+   - **AppleTalk host name** — Your computer’s hostname (type `hostname -s` to see it) is used as your computer’s AppleTalk server hostname.

+   - **Authentication** — Netatalk will allow users to connect using a guest login (*nobody* user) with no password, a clear-text password, or an encrypted password (Diffie-Hellman style authentication).

+   - **Guest user** — A guest user can connect without entering a password and access shared volumes that are open to the world. This guest user is assigned to the Linux *nobody* user name. (By default, no guest shares are set up.)

+   - **Daemon processes** — Netatalk starts *daemon* processes to manage your AppleTalk network interface (`atalkd` daemon), start the AppleTalk print sharing service (`papd` daemon), and start the AppleTalk filing protocol (`afpd` daemon) for sharing volumes.

+   5. **Configure server settings** (`/etc/afp.conf` file) — Configuring `afpd.conf` lets you set up specific settings for your netatalk server (you can even have multiple, virtual servers configured that each look different to the outside world). The contents of the `afpd.conf` file affect how the AppleTalk filing protocol daemon (`afpd`) shares its volumes with Mac clients.

+   6. **Set up users** — The netatalk server can rely on the Linux users you add to the computer (using clear-text passwords), then limit access to your shared volumes based on those permissions. Or, you can configure netatalk to use encrypted passwords to validate users.

+   7. **Share volumes** (`/etc/afp/AppleVolumes.default` file) — When netatalk starts, each user with a valid Linux login to your computer can, by default, access his or her own home directory as an AppleTalk share from a Mac client. You can (and probably will) have more shared volumes by configuring them in the `AppleVolumes.default` file.

+   8. **Securing shared volumes** — Netatalk can take advantage of Linux security features to protect shared volumes. You can secure volumes at the host, user, and file and directory level.

+   9. **Share printers** (`/etc/afp/papd.conf` file) — Netatalk can share any printer you have connected to Linux (or otherwise configured locally) by adding a definition to the `papd.conf` file. No printers are shared until you add them.

As you work with your shared volumes and printers, you will find that maintenance issues arise from time to time. In particular, you should refer to the following sections: “File- and directory-level security” (for dealing with hidden attribute files and directories), “Sharing files with netatalk and Samba” (to share the same directories from netatalk and Samba), and “Troubleshooting netatalk” (for general troubleshooting tips).

# ## Starting netatalk

Start up netatalk as you would most Linux network services: from a start-up script. The netatalk script is called `atal` (`/etc/init.d/atal`). To turn it on, type the following as root user: