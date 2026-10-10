form1: vparload -all
form2: vparload -auto
form3: vparload -p vp_name [ b kernelpath] [ o boot_options]
[-B hardware_path]

form1 boots all vPar. form2 boots all vPar that have the autoboot attribute set. form3 allows you to specify options such as: the kernelpath to boot; the boot_options, such as “is” for single user mode; or hardware_path, which specifies the boot device to be used for the vPar.

Issuing the /stand/vpmon command at the ISL> prompt gives us the MON> prompt. To use vparload to boot all Virtual Partitions on a server we would issue the following command:

MON> vparload -all

To use vparload to boot Virtual Partition symbol1, we would issue the following command:

MON> vparload -p symbol1

You could perform the steps to load both the vpmon and virtual partition symbol1 from ISL with the command below at the ISL prompt:

ISL> hpxs /stand/vpmon vparload -p symbol1

This command boots both vpmon and then symbol1. You may perform experimentation with the kernels of the vPar’s on your system and have to boot different kernels. The following example shows booting from a kernel called vmunix_test1: