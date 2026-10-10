```
```
},
};

/* Driver Initialization */
static int __init
mycard_audio_init(void)
{
        /* Register the platform driver and device */
        platform_driver_register(&mycard_audio_driver);

        mycard_device = platform_device_register_simple("mycard_ALSA",
				-1, NULL, 0);
        return 0;
}

/* Driver Exit */
static void __exit
mycard_audio_exit(void)
{
        platform_device_unregister(mycard_device);
        platform_driver_unregister(&mycard_audio_driver);
}

module_init(mycard_audio_init);
module_exit(mycard_audio_exit);
MODULE_LICENSE("GPL");
```
```

# ALSA Programming

To understand how the user space alsa-lib library interacts with kernel space ALSA drivers, let's write a simple application that sets the volume gain of the MP3 player. We will map the alsa-lib services used by the application to the mixer control methods defined in Listing 13.1. Let's begin by loading the driver and examining the mixer's capabilities:

```
```
bash> amixer contents
...
numid=3,iface=MIXER,name="MP3 Volume"
        ; type=INTEGER,..
...
```
```

In the volume-control application, first allocate space for the alsa-lib objects necessary to perform the volume-control operation:

```
```
#include <alsa/asoundlib.h>
snd_ctl_elem_value_t  *nav_control;
snd_ctl_elem_id_t      *nav_id;
snd_ctl_elem_info_t     *nav_info;

snd_ctl_elem_value_alloc(&nav_control);
snd_ctl_elem_id_alloc(&nav_id);
snd_ctl_elem_info_alloc(&nav_info);
```
```