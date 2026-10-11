# # Questions & answers

All your technical problems solved

![](bbox=[0.88, 0.09, 0.99, 0.14])

It’s certainly possible to do this, and it doesn’t require a huge amount of messing around to accomplish either. First of all, boot into a live Linux environment from a disc or USB storage.

Use `fdisk -l` and make a note of the cylinders, heads and sectors, and then edit the image file **sda-csh.s** with these new details. Next, use:

```
`$ parted /dev/sda ‘unit s’ print`

*...*noting down the first few lines, and then edit the file **sda-p.p** to match this.
```

Finally, sync/restart and the restore the image with GnomeDisks and you should be all set. Next time, you could always shrink a partition to fit the destination before cloning, which should make it a little easier.

# ## Converted

I’ve been trying to follow a guide on converting an MKV to an AVI using MEncoder. It seems to work just fine, but I keep getting problems where it just plays the audio on some devices. Here’s what I’m doing to convert the video, weis:

```
`$ mencoder abc.mkv -oac pcm -ovc xvid -xvidencopts bitrate=888 -sub ITC0101_srt -subfont-text-scale 3 -o zzzz.avi`
```

It works fine on my PC, but on my DVD player, which has no problem with these codecs usually as far as I’m aware, it just doesn’t work. Am I missing something with my command, or is there another way I should be going about doing this?

**Tim Duley**

No, your command seems to be fine, it’s most likely an issue with MEncoder and the limited codecs on the DVD player. You might be better off trying FFmpeg, though,

![](bbox=[0.15, 0.78, 0.36, 0.92])

and you can do so with the following commands:

```
`$ ffmpeg -i input.mkv -vcodec libxvid -qscale 5 -s 640x272 -aspect 40:17 -r 23.976 -g 240 -bf 2 -acodec libmp3lame -ab 160k -ar 48000 48000 -ac 2 -pass 1 -an -f rawvideo -v /dev/null`
```

```
`$ ffmpeg -i input.mkv -vcodec libxvid -qscale 5 -s 640x272 -aspect 40:17 -r 23.976 -g 240 -bf 2 -acodec libmp3lame -ab 160k -ar 48000 -async 48000 -ac 2 -pass 2 -f avi Outlander-GS.avi`
```

This should give you a little more control over what you’re outputting, and hopefully work a bit better with your DVD player.

# ## Batch download

Every now and then I come across a website directory that has a load of individual files I need to download residing within it. I used to use a Firefox add-on to select and download them all in one. However, I’m wanting to know if there’s a more universal way of me doing this without having to get extra add-ons for my browser?

**Colin Stilt**

![](bbox=[0.36, 0.55, 0.65, 0.7])

> It’s most likely an issue with MEncoder and the limited codecs on the DVD player

# ## Minty Apple

My parents have finally decided to join this century and get a proper computer rather than relying on me or library computers to get their information. As family tech support, I’ve told them I’ll get them set up with a new system they can use for emails and such. Because they’ve never really used computers much at all, I wanted to set up a Linux Mint system for them. However, the only issue I have is finding spare hardware to get that going. I did find that I have a Mac Mini lying around, though, so I thought about putting Linux on that. However I seem to recall it’s not as easy as just putting the live disc in and installing as I found out.

I’m not too bothered about losing OS X, and would much prefer my parents use Mint anyway. How do I get it installed on there?

**Jeff Vincent**

While Mint and its Ubuntu base have tools to install on Secure Boot systems that use UEFI, it requires the use of legacy modes to get it work normally. But we don’t have that luxury with a Mac, so you need to do a little more. The main issue is that it uses a different partition table that won’t work with Mint, so the easiest thing to do if you’d mind losing OS X is convert it to something more Linux friendly.

Make sure any files you want to keep are backed up, as this method will format the hard drive. Burn a live CD or DVD of Mint and put it in your optical drive. Restart the Mac and hold down the Option key to bring up the boot selection screen, and of course select CD. Boot into the live environment by choosing **Try Linux Mint**.

When Mint loads up, you’ll next need to open **GParted**. By default it should select the Mac’s hard drive, so click Device on the menu bar and then go to Create Partition Table. A warning will pop up, and then you’ll want to click the Advanced triangle. From here you’ll be able to create a new partition table format, this time as MS-DOS.

![](bbox=[0.65, 0.7, 1.0, 0.78])

After that is done, you can install Linux Mint however you wish. We’d suggest using Cinnamon if your parents are more used to Windows systems, and show them how to install apps from the Software Centre.