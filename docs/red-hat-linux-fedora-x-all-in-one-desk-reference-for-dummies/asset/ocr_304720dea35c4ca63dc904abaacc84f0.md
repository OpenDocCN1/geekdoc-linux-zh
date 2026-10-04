# 106 Preparing a Fedora Core DVD

+   4. Copy the isolinux directory and the .discinfo file from the first CD ISO file to the /tmp directory (which happens to be the current directory).

Type the following command to copy the files:

```
cp -af IS01/isolinux IS01/.discinfo .
```

Don't miss that single period at the end of the command!

+   5. Open the .discinfo file in a text editor and edit the fourth line as follows:

1,2,3,4

That lists the numbers of CD ISO images that are being included on the DVD ISO image. Save the .discinfo file after editing that line.

+   6. Create the DVD ISO out of the four CD files.

Type the following mkisofs command to create a new ISO file named fedora-core-dvd.iso:

```
mkisofs -o fedora-core-dvd.iso \
  -V 'Fedora Core DVD' \
  -b isolinux/isolinux.bin -c isolinux/boot.cat \
  -no-emul-boot -boot-load-size 4 -boot-info-table \
  table \
  -R -m TRANS.TBL \
  -x IS01/.discinfo \
  -x IS01/isolinux \
  -graft-points IS01 \
  .discinfo=.discinfo isolinux=isolinux \
  Fedora=/IS02/Fedora \
  Fedora=/IS03/Fedora \
  Fedora=/IS04/Fedora
```

You can burn the DVD ISO file onto DVD media.

# Burn DVD ISO file onto DVD media

Assuming that the DVD ISO file is named fedora-core-dvd.iso, follow these steps to burn the DVD ISO file onto the DVD:

+   1. Use the cd command to change the current directory to where the DVD ISO file is located.

+   2. Place a blank DVD media into the DVD recorder.

+   3. Type the following growisofs command to start burning the DVD:

```
growisofs -Z /dev/scd0=fedora-core-dvd.iso
```