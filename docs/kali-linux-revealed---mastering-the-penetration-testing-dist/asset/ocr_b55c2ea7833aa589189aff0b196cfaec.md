is no newer version installed or available in another distribution. A package of priority between 501 and 990 will only be installed if there is no newer version installed or available in the target distribution. With a priority between 990 and 1000, the package will be installed except if the installed version is newer. A priority greater than 1000 will always lead to the installation of the package even if it forces APT to downgrade to an older version.

When apt /etc/apt/preferences, it first takes account the most specific entries (often specifying the concerned package), the more generic ones (including all packages of a distribution). If several generic entries exist, the first it is used. The available selection criteria include the package name and the source providing it. Every package source is identified by the information contained in a Release file that APT downloads together with the Packages files. These files specify the origin, unless "Kali" for the packages from Kali's official mirrors or "Debian" for the packages from Debian's official mirrors, the origin can also be a person or an organization's name for third-party repositories. The Release file also provides the name of the distribution together with its version. Let's have a look at its syntax through some realistic cases of this mechanism.

| Priority | The corresponding packages will almost never be installed because their default APT priority is 1. This is of course a specific case, designed to keep users from installing bleeding packages by mistake. The packages can only be installed by typing apt package=Kali-bleeding-edge assuming that you are aware of the risks and potential boundaries of life on the edge. It is still possible (though not recommended) to treat packages of kali-bleeding-edge/experimental like those of other distributions by giving them a priority of 500. This is done with a specific entry in /etc/apt/preferences: |
| --- | --- |
| Priority of Kali-Bleeding-edge and Debian Experimental | Package: *
Pin: release a=kali-bleeding-edge
Pin-Priority: 500

Let's suppose that you only want to use packages from Kali and that you only want Debian installed when explicitly requested. You could write the following entries in the /etc/apt/preferences file (or in any file /etc/apt/preferences.d):

```
Package: *
Pin: release o=Kali
Pin-Priority: 900
```

```
Package: *
Pin: release o=Debian
Pin-Priority: -10
```