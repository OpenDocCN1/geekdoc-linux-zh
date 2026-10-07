# v4.33
A Comprehensive Beginner's Guide to Linux as a Digital Forensic Platform

12884901888 bytes ( 12 G ) hashed ( 100% ), 32.435 s, 379 M/s

input results for file `stdin`:
25165824 sectors out
8f6cec10ae87d6ff4590ba809ba51385679738ed (shal)

output results for file `ncgzuncomp.raw`:
25165824 sectors out
[ok] 8f6cec10ae87d6ff4590ba809ba51385679738ed (shal)

dc3dd completed at 2017-05-06 13:46:55 -0400

A couple of things to notice here. First, our hashes match. We successfully read a device, compressed the data, piped it over a network, decompressed and wrote an image file. The reason we do this is to some time. Have a look at the time it took to image (from the log file) and compare it against our earlier using netcat without compression:

Without compression (from previous exercise): (dd | netcat)
12884901888 bytes ( 12 G ) copied (%%), 747.491 s, 16 M/s

With compression: (dd | gzip | netcat)
12884901888 bytes ( 12 G ) copied (%%), 522.142 s, 24 M/s

Almost four minutes savings by compressing the data before transporting it. Keep in mind that the usefulness of this is dependent on your particular bottlenecks. On a local network, by crossover cable, and writing to a USB 2.0 drive, compressing the network may have little impact. If you are imaging over an enterprise network, remotely, you may see a performance gain from compression. Your results may vary, but be aware of the technique.

# Preparing a Disk for the Suspect Image

We've already covered simple acquisitions, and media sanitization is a step that is normally performed before you conduct evidence collection. It is introduced here

145