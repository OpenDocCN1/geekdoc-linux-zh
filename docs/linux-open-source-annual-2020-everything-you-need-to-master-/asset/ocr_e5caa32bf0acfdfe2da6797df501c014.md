# ## Install and first run

Does the installer welcome you?

![](bbox=[0.51, 0.09, 0.93, 0.26])

**A** ntergos impresses right from the outset with the stylish **Cnchi** installer. You can choose to set up popular applications and desktops. These all need to be downloaded, which puts the kibosh to offline installs, but it does do installees the courtesy of offering to find the fastest mirrors. If you're worried about the install going south and having to start over then you can opt to create a recovery partition on the target device. This is a nice touch, but mercifully not one we had reason to use. You can even choose between GRUB2 and systemd-boot, encrypted installs and even using ZFS.

Manjaro's live medium starts with a slightly spartan menu for selecting keymaps, free vs non-free drivers or adding kernel parameters. Once the Calamares (see **LF293**) installer fires up we're met with the usual options (LVM and encryption) and you can choose between using your drive, installing alongside other OSes, or manual partitioning. Once you boot into Manjaro, a welcome screen displays release information and provides links to the Wiki. There's a handy tool for installing popular apps, too. Netruntime, being a Manjaro descendant, has a similar installation process. Newcomers might be a little upset to find the Readme icon on the desktop takes them to a 404 page, with a mixed content warning, but this is a cosmetic thing. KaOS also uses the Calamares installer. XFS is a slightly left-field choice for a default filesystem, but why not? Once installed the Croeso (Welsh for 'welcome') tool greets you and provides shortcuts to documentation and common system settings. This is handy if you don't know where Plasma hides these things, and even if you do it's nice to have them all in one place. Creoso has a few more options than Manjaro's welcome tool.

**ABiF**, Archlabs' Ncruses installer isn't newbie-friendly, but offers the same options as Antergos and carries out a full system update before rebooting. Once the live medium hasn't been updated since July 2018, this is a fairly lengthy process. Once you reboot, a menu enables you to install popular applications, fonts and so forth. If you don't like logging in from the console, the LightDM display manager is readily available from here, too.

# ### VERDICT

| ANTERGOS | 9/10 |
| --- | --- |
| MANJARO | 8/10 |
| ARCHLABS | 6/10 |
| NETRUNNER ROLLING | 8/10 |
| KADS | 7/10 |
| MANJARO | 8/10 |

Antergos' Cnchi sets a new standard for Linux installers. ArchLabs' textual experience can't compete, but console warriors won't mind.

# ## Repositories

How do these repos stay up to date?

![](bbox=[0.51, 0.61, 0.93, 0.79])

**B** e mindful that we're using the stock Arch repositories as a baseline here, and short of packaging things yourself or using snaps this is pretty much the fastest way to get the latest upstream releases.

Manjaro takes a leaf out of Debian's book, offering Stable, Testing and Unstable branches. The Unstable packages track around three days behind the Arch repo, which should be fresh enough for anyone. Packages make it into stable "when they're ready", and this is usually pretty swift unless some exigency arises. At the time of writing there's a stability issue with new versions of Systemd, but otherwise we found no major differences. Netruntime Rolling is based on Manjaro's Stable channel (though a handful of custom packages come from its own repo), so it can enjoy the 12,000 odd packages in Manjaro's repos.

KaOS tends to lag behind a little further, and the only graphical apps you'll find in its repos are Qt ones, such as its KDE Plasma focus. If you need anything else, you'll have to build it yourself. You can do so from the KaOS Community Packages repo, which given KaOS's limited repos, vastly widens its scope of interest. KaOS uses Plasma 5.14, compared to Netruntime's Plasma 5.12, and both currently use version 18.08 of the KDE applications suite, hopefully the just-released 18.12 apps bundle blesses these KDE distros soon. Finally, Antergos maintains a handful of its own packages, but otherwise relies on the Arch Linux repos, and ArchLabs uses exclusively the Arch repos.

KaOS has only a couple of thousand packages in its repositories. This is a fraction of what you get with Arch, and maybe all you need.

# ### VERDICT

| ANTERGOS | 8/10 | MANJARO | 9/10 |
| --- | --- | --- | --- |
| ARCHLABS | 8/10 | NETRUNNER ROLLING | 7/10 |
| KADS | 8/10 |  |  |

Manjaro's channels cater to all users, and their generous repositories are almost as well-stocked as Arch's.