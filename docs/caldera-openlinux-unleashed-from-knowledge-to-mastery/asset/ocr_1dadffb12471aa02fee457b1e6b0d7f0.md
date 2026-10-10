# # Lossless Audio Encoding Using shorten

Let's face it: Although many people will be completely happy with a good lossy audio compressor, there will always be others who will never be satisfied if even so much as a bit of the original data is thrown away. For these people, whether audiophiles, musicians, or sound engineers, MPEG 1 Layer 3 just won't do (at least not for the majority of their needs). Fortunately, those people have a friend at the Cambridge University Engineering Department, Dr. A. J. Robinson. Dr. Robinson has not only written a high-quality lossless waveform compressor called shorten, but he has released the source code under a freely distributable noncommercial license, making his technology available to us. shorten is an excellent compressor, typically able to compress CD-quality audio to between one-half to three-quarters of its original size. We now begin our investigation of a sound compressor that is perfectly acceptable even for perfectionists.

# ## shorten—Where to Get It

To download the Linux version of shorten, visit Tony's Cambridge University Web site, located at [http://www.eng.cam.ac.uk/~ajr](http://www.eng.cam.ac.uk/~ajr), and click the speech and audio coding link. You will then be able to download the UNIX version of shorten, as well as review an online technical report on the technology. After downloading shorten, perform the following steps to compile it under Linux:

```
```
> cd /tmp
> tar xzvf /path/to/archive/shorten.tar.gz
> cd shorten-2.3a
> make
```

```

Then, as root:

```
```
> make install
```

```

# ## shorten—How to Use It

Installation is complete, and shorten is now ready to use. But before we begin, let's create a batch file that will help us play back ".shn compressed files. As root, change directories to `/usr/local/bin`, and create a file called `shnp` that contains the text in Listing 29.1.

![](bbox=[0.85, 0.65, 0.98, 0.8])