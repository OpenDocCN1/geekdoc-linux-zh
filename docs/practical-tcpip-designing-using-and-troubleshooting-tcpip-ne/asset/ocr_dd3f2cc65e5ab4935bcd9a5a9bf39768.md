# # Appendix 26 Organizing your software downloads

This method of archiving downloaded software has worked well for us for years.

+   • we keep a dedicated disk for archiving downloads. This is on our main file server, mounted as /r for "aRCives"

+   • all Linux machines NFS-mount the archive as local directory /r (so it has the same name on every machine – local or remote)

+   • we run Samba on the main file server, and share the /r directory as share name archives. All Windows machines map this as local drive R:. (We can't use drive letter A: as that's the name of the floppy drive, which is why we can't mount the archive as /a or call it archives.)

+   • on each Windows machine we keep a local directory called archive-duplicate. We use this as a cache of a few important items from the main archive that we might need when this machine's networking is broken, e.g. Windows service packs and network card drivers

+   • the archive has grown over the years, and it's too big and awkward to keep in a single directory, so we break it into subdirectories. Whenever we download from a site, we save the download in a directory named after the site (ignoring the initial www, etc.). To avoid having a huge list of sites, we group the site names further by initial letter, e.g. if we download a file from www.debian.org, we save it in /r/d/debian.org/filename

+   • in each directory we maintain a "readme" file, saying what each file is, and giving its URL. (We use the filename read-uit.txt for this, in case we download a file called readme or readme.txt.)

+   • if we need to unpack a Zip or a tar file, we do it into a subdirectory called junk, and we often build and install software from junk. However, we never make any changes (or at least, any changes that we'll need again) to anything in a junk directory. That way we know we can always delete it if we need some extra disk space, because we can always unpack again from the original Zip or tar archive whenever we want.

![](bbox=[0.1, 0.65, 0.78, 0.98])