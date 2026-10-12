```
# wait 20 seconds (200 10ths) for user to select
# the entry to load
timeout=200



#
# deafault entry
#
image=/boot/vmlinuz
  label=linux
  root=/dev/hda1
  read-only


#
# golden entries
#
image=/boot/vmlinuz-2.2.16
  label=linux.golden
  root=/dev/hda1
  read-only


#
# older entries
#
image=/boot/vmlinuz-old
  label=linux.old
  root=/dev/hda1
  read-only



#
# end of file
```

In this file, I have granted myself a couple of options for safety. First, when Linux first boots up, it normally stops at the LILO: prompt. I have given myself 20 seconds in which to choose the type of kernel that I wish to boot. At that prompt, I can press the Tab key to see the available choices: linux, linux.golden, and linux.old. If your machine is a dual- or triple-boot machine, you might also include settings for a particular Windows version or some other operating system. It is in lilo.conf that you can enter settings for alternative boot partitions.