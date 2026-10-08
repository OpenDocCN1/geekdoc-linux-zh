| URL | Internet Site |
| :--- | :--- |
| [fedoraproject.org/wiki/Distribution/Download](fedoraproject.org/wiki/Distribution/Download) | Download page for the latest Fedora releases |
| [fedoraproject.org/Download/mirrors.html](fedoraproject.org/Download/mirrors.html) | Page listing Fedora mirrors |
| [download.fedora.redhat.com/pub/fedora/linux/](download.fedora.redhat.com/pub/fedora/linux/) | Fedora Yum repository for Fedora software |
| [download.fedora.redhat.com/pub/fedora/linux/updates](download.fedora.redhat.com/pub/fedora/linux/updates) | Fedora Yum repository for Fedora updates |
| [linux.duke.edu/projects/yum](linux.duke.edu/projects/yum) | Yellow Dog Updater, Modified (Yum) update tool, with listings of Yum repositories for updating Fedora Linux |
| [moim.connectiva.com.br/AptRpm](moim.connectiva.com.br/AptRpm) | APT-RPM Red Hat repository for APT-enabled RPM packages (see Chapter 4) |
| [rpm.livna.org/fedora](rpm.livna.org/fedora) | Fedora applications not included with the distribution due to licensing and other restrictions. This is an official extension of the Fedora Project. |
| [www.freshrpms.net](www.freshrpms.net) | Linux multimedia applications and support libraries; specifically lists Fedora-version RPM packages |
| [sources.redhat.com](sources.redhat.com) | Open source software hosted by Red Hat |
| [torrent.fedoraproject.org](torrent.fedoraproject.org) | Fedora BitTorrent site for BitTorrent downloads of Fedora distribution ISO images |

enable or disable write support. Be careful of this option. It should work but is not guaranteed. There are also third-party NTFS support packages from Livna and freshrpms. They are not compatible. Use one or the other.

Due to licensing restrictions, multimedia support for popular operations like MP3, DVD, and DivX is not included with Fedora distributions. A Fedora Project-associated site, rpm.livna.org/fedora, does provided support for these functions. You can download free licensed MP3 gstreamer plugin from www.fluendo.com. Any software you do not find at those sites can usually be found at freshrpms.net. Fedora does not provide support for the official Nvidia- or ATI-released Linux graphics drivers. Support for these can be found at rpm.livna.org/fedora (see Chapter 4). Fedora does include the generic X.org Nvidia and ATI drivers, which will enable your graphics cards to work.

> TIP The software management tools, Program Manager and PUP, will list software from all configured Yum repositories. Initially these include Fedora, update, and development. If you add configurations for rpm.livna.org or freshrpms.net, their software will also be listed and managed by Program Manager and PUP.

# Third-Party Linux Software Repositories

Though almost all application should be included in the Fedora software repository, you could download and install software from third-party repositories. Always check first to see if the software you want is already in the Fedora repository. Open Add /Remove Software