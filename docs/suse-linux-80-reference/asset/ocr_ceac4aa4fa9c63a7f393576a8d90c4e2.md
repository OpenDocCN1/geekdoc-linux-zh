We are mainly concerned with the parameters required for a successful installation, but there are other parameters intended for special purposes. Uppercase letters are significant.

A complete introduction to possible kernel parameters can be found after installation in the `BootPrompt-HOWTO` in `/usr/share/doc/howto` and in the kernel sources in the file `/usr/src/linux/Documentation/kernel-parameters.txt`.

# Kernel Parameters at the Boot Prompt

The parameters listed in this section can only be passed to the kernel, for example, at the SYSLINUX prompt (boot disk included), at the LILO prompt, or with loadlin.

If you plan to install one of these drivers as a module, look at the parameters in Section *modprobe Parameters* on page 255.

> > **Note**
> >
> > All parameters must be entered directly one after another, separated by commas. There should be no spaces between the parameters.

For example, to enter the parameters for aha1542 at the boot prompt, enter `linux aha1542=0x300`. Keep in mind that you always have to precede the parameters with the boot configuration’s name. On SuSE boot disks, this is the configuration with the name `linux`.

# General boot parameters

Certain parameters can be used to control the overall behavior of the Linux kernel.

+   - *Reboot mode* (shutting down Linux)
+     `reboot={mode}`
+     Here, you have the following values for `{mode}`:

| Variable | Values / Meaning |
|---|---|
| `warm` | warm reboot (no memory check) |
| `cold` | cold reboot (with memory check) |
| `bios` | BIOS reboot |
| `hard` | CPU crash reboot (triple fault) |

*Example:* `reboot=cold`

This boots the machine after shutdown as if the reset button had been pressed.