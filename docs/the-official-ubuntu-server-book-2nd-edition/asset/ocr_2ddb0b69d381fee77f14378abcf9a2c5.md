![](bbox=[0.31, 0.12, 0.88, 0.52])

Figure 5-15 Multiboot system in action

# TIP

When entering your password, nothing is displayed on the screen, although your password is still being read by the computer. The password is not displayed for security reasons, but it is also not obfuscated. This prevents people who may be looking over your shoulder from seeing how many characters your password has.

# TIP

It is possible here to update the SSH keys by simply restarting the network interface, using a command similar to the following one. You will need to replace <iface> with the interface identifier, usually something like eth0 or eth1.

```
sudo ifdown <iface> && sudo ifup <iface>
```

Once completed, your SSH keys will be updated, and after the clients reboot, they should be able to log in again.

# Local Devices over LTSP

Since Ubuntu Edgy 6.10, Edubuntu has included the update to LTSP to allow what are called local devices. Plugging a USB storage device into a thin client machine, for example, will trigger the local devices mechanism, and the device will be correctly mounted and shown on the desktop of the client machine.