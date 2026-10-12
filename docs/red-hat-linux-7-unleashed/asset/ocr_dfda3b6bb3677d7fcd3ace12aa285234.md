```
vc=$1 #Which VC to dump
#Extract the VC's width from the second byte of the vcsa device
#The `unpacx` expression extracts the value of the second
#character of the input (the vcsa device).
Width=`dd if=/dev/vcsa bs=1 count=1 skip=$i 2>/dev/null|hexdump -e "'\%d'"`
#Use dd(1) to convert the output now that we know the width
dd cbs=$i width conv=unblock</dev/vcsa${vc} 2>/dev/null
```

# ## Summary

This chapter introduced character and block devices, filesystem administration, and gave an overview of the hardware that can be accessed via the special files in the /dev directory.

One of the difficulties in writing a chapter like this is that things are constantly changing. For example, soon we will be using ext3 instead of ext2 for the standard filesystem type. The kernel maintainers and distribution maintainers are trying to keep things in line enough so that ordinary computer users can use this stuff, but at the same time allow flexibility so that new and improved “stuff” can be designed. Many of the areas that the Linux community has focused on throughout the years have fallen under the section devices and filesystems. Therefore, as the standards switch from using /dev/cua* devices to using /dev/ttyS* devices, and so on, documentation needs to be constantly updated.

In the meantime, programmers are working their little penguins to the wing tip trying to design easier tools to help remove some of the difficulty with using and configuring Linux. They have come a long way with tools such as usermount and fsconf, but they still have a long way to go before they are finished.

You can find further information from the Linux Documentation Project material at http://www.linuxdoc.org/. Much of the LDP material is also provided on the CD-ROMS accompanying this book.