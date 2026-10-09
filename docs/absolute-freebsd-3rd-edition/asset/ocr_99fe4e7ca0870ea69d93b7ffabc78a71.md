Every FreeBSD release eventually reaches *End of Life* (*EoL*) and loses support. The security team stops producing patches and new packages are no longer available. The older release will reach *EoL* before the newer version. If you install FreeBSD 10.4 today, you'll need to upgrade to 11 at some point—but by then, you'll be upgrading to something that's not a .0 release.

FreeBSD averages two production releases at a time. This isn't an inviolate rule, only observed behavior. Sometime around when the 12.0 release escapes, the 10 branch will reach *EoL*.

I personally will run FreeBSD .0 releases, but having been burned with other operating systems before, I sympathize with the folks who categorically reject .0 versions. If you've never used FreeBSD before, I recommend installing the most recent production release. It has the latest device drivers and newest features.

Follow the download link and grab your chosen version.

# **Choosing Installation Images**

You can choose between several different formats of FreeBSD installation media. All installation media is available both compressed with `xz(1)` and uncompressed. If you can conveniently extract .xz files, download the compressed versions. This saves the donated bandwidth and reduces download time. Any modern operating system can either handle .xz files natively or has add-on software for the task.

FreeBSD offers two styles of installation media. The first contains only enough to boot the FreeBSD installer and bring up the network. The installer then downloads the operating system files from a FreeBSD mirror site. If you're going to do multiple installs of the same FreeBSD version, though, you're better off downloading an installer that includes the operating system files.

The installer comes in both optical disk (*iso*) and flash (*img*) formats. Choose the format that fits your system. If you're installing a virtual machine, an ISO is probably simplest.