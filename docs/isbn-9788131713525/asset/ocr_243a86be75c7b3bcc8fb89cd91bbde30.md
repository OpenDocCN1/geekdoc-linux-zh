jbd module. The modprobe utility can discover this relationship and load the dependent modules in the proper order. The following command loads both the jbd.ko and ext3.ko driver modules:

```
$ modprobe ext3
```

The modprobe utility has several command line options that control its behavior. As we saw earlier, modprobe can be used to remove modules, including the modules upon which a given module depends. Here is an example of module removal that removes both jbd.ko and ext3.ko:

```
$ modprobe -r ext3
```

The modprobe utility is driven by a configuration file called modprobe.conf. This enables a system developer to associate devices with device drivers. For a simple embedded system, modprobe.conf might be empty or might contain very few lines. The modprobe utility is compiled with a set of default rules that establish the defaults in the absence of a valid modprobe.conf. Invoking modprobe with only the -c option displays the set of default rules used by modprobe.

Listing 8-8 represents a typical modprobe.conf, which might be found on a system containing two Ethernet interfaces; one is a wireless adapter based on the Prism2 chipset, and the other is a typical PCI Ethernet card. This system also contains a sound subsystem based on an integrated Intel sound chipset.

# ## Listing 8-8

Typical modprobe.conf File

```
$ cat /etc/modprobe.conf
alias eth0 orinoco_pci
options eth0 orinoco_debug=9
alias eth0 e100
alias snd-card-0 snd-intel8x0
options snd-card-0 index=0
$
```

When the kernel boots and discovers the wireless chipset, this configuration file instructs modprobe to load the orinoco_pci device driver, bound to kernel device eth1, and pass the optional module parameter orinoco_debug=9 to the device driver. The same action is taken upon discovery of the sound card hardware. Notice the optional parameters associated with the sound driver snd-intel8x0.