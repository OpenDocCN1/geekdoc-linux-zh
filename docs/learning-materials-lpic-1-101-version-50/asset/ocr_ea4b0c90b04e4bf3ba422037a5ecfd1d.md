```
```
rt61pci    32326  0
rt2x00pci  13083  1 rt61pci
media      20840  1 videodev
rt2x00mmio 13322  1 rt61pci
hid_dr     12776  0
snd_mpu401_uart  13992  1 snd_ice1712
rt2x00lib  67108  3 rt61pci,rt2x00pci,rt2x00mmio
snd_rawmidi 29394  2 snd_usbmidi_lib,snd_mpu401_uart
```
```

The output of command `1smod` is divided into three columns:

# ## Module

Module name.

# ## Size

Amount of RAM occupied by the module, in bytes.

# ## Used by

Depending modules.

Some modules require other modules to work properly, as is the case with modules for audio devices:

```
```
$ 1smod | fgrep -i snd_hda_intel
snd_hda_intel       42658  5
snd_hda_codec      155748  3 snd_hda_codec_hdmi,snd_hda_codec_via,snd_hda_intel
snd_hda            81999  3 snd_hda_codec_hdmi,snd_hda_codec,snd_hda_intel
snd_page_alloc      13852  2 snd_pcm,snd_hda_intel
snd               59132  19
snd_hwdep,snd_timer,snd_hda_codec_hdmi,snd_hda_codec_via,snd_pcm,snd_seq,snd_h
da_intel,snd_seq_device
```
```

The third column, `Used by`, shows the modules that require the module in the first column to properly work. Many modules of the Linux sound architecture, prefixed by `snd`, are interdependent. When looking for problems during system diagnostics, it may be useful to unload specific modules currently loaded. Command `modprobe` can be used to both load and to unload kernel modules: to unload a module and its related modules, as long as they are not being used by a running process, command `modprobe -r` should be used. For example, to unload module `snd-hda-intel` (the module for a HDA Intel audio device) and other modules related to the sound system: