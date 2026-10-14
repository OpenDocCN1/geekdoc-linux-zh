# Adding a new repository key

Sometimes a repository contains *digitally signed* packages. Signing is a method of ensuring packages haven’t been tampered with, or forged. The programmer stamps each package with an ID that only she can create. This is done using a cryptographic key, the public component of which is offered for download and must be installed by end users.

You can add the public key to your system in the following way:

+   1. The key is usually offered for download at the same place you’ll find the package—it will have an `.asc` or `.gpg` file extension. Right-click it and select Save As, then save it to disk. Be sure to download the key only from the package creator’s website, and not a mirror site. After all, it’s possible the key may also have been tampered with.
+   
+   2. In the Software Sources program, click the Authentication tab and click the IMPORT KEY FILE button. Then navigate to the file you saved. Click OK when done.

To import the key at the command-line, type the following, replacing `keyfile.gpg` with the name of the downloaded file:

```
sudo apt-key add keyfile.gpg
```

> **NOTE**  If the packages you attempt to install come from a third party repository and *aren’t* digitally signed, you may see a warning during installation saying the packages can’t be authenticated. This is there to warn you that you’re installing non-official packages, but is usually nothing to worry about.

# Compiling from source code

The nature of Linux means that virtually all available software is *open source*—the source code is free for people to view, use, and even adapt into new software.

In the heyday of Unix back in the 1970s/80s, the *only* method of installing new software was to take the source code and **compile** it—manually turn it into a *binary* that can be run day-to-day.

Although ready-made and pre-compiled software packages rule the roost when it comes to Ubuntu software installation, you may find some Linux software is only available as source code. This is often the case with new hardware drivers that must be manually compiled in order to work correctly with the kernel program.