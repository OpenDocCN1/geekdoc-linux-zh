> Tip
> The contents of the **Boot label** column show what you will need to enter at LILO's `boot:` prompt in order to boot the desired operating system. Should you forget the boot labels defined on your system, press [Tab] at LILO's `Boot:` prompt to display a list of defined boot labels.

There is also a column labeled **Default**. Only one partition will contain an asterisk under that column. The partition marked as the default will be the partition LILO will boot if there is no user input during the boot process. Initially the root partition for your Red Hat Linux installation will be selected as the default. If you’d like to change this, use the arrow keys to highlight the partition you’d like to make the default, and press [F2]. The asterisk will move to the selected partition. When you’ve finished, select **OK**, and press [Space].

# ### 10.11.3 SMP Motherboards and LILO

If the installer detects a symmetric multi-processor motherboard on your system, it will automatically create two `lilo.conf` entries: `linux`, the default, boots the system in SMP mode and `linux-up` boots the system in uni-processor mode.

# ## 10.12 Naming Your Computer

The **Hostname Configuration** dialog prompts you to enter a name for your computer (called a **hostname**).