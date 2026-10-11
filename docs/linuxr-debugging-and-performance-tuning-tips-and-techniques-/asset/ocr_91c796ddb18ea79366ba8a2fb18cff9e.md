$ df

| | | | Used | Available | Use% | Mounted on |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| Filesystem | 1K-blocks | 1K-used | 1K-free | | | |
| /dev/hda2 | 6198436 | 5136020 | 747544 | 88% | | / |
| /dev/hda5 | 61431520 | 27720248 | 30590648 | 48% | | /d |
| none | 256616 | 0 | 256616 | 0% | | /dev/shm |

The tmpfs filesystem type provides a RAM disk, a portion of memory used as if it were a disk. Furthermore, the tmpfs filesystem uses the Linux kernel’s virtual memory mechanisms to allow it to grow beyond a fixed size limit. If you have lots of RAM in your system, this approach can provide a noticeable speedup. To test performance we started with the /usr/share/dict/linux.words file, which is a sorted list of correctly spelled words, one per line. We then randomized this file so that it was no longer sorted and created a larger file containing 500 copies of the random version of the file:

$ ls -l /tmp/randwords.big

-rw-r--r-- 1 arnold devel 204652500 Sep 18 16:02 /tmp/randwords.big

How many words? Over 22 million!

We then sorted the file, first using the default /tmp directory, and then with TMPODR set to /dev/shm:<sup>5</sup>

$ time sort /tmp/randwords.big > /dev/null

real 1m32.566s
user 1m23.137s
sys 0m1.740s

$ time TMPDIR=/dev/shm sort /tmp/randwords.big > /dev/null

real 1m28.257s
user 1m18.469s
sys 0m1.602s

Interestingly, using the RAM disk was only marginally faster than using regular files. (On some further tests, it was actually slower!) We conjecture that the kernel’s buffer cache (see Section 4.6.2, “Creating Files With creat(),” page 109) comes into the picture, quite effectively speeding up file I/O.<sup>6</sup>