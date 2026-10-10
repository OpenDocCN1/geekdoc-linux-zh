
One possible hardware implementation of the device shown in Figure 13.4 is by using a PowerPC 405LP SoC and a Texas Instruments TLV320 audio codec. The CPU core in that case is the 405 processor and the on-chip audio controller is the Codec Serial Interface (CSI). SoCs commonly have a high-performance internal local bus that connects to controllers, such as DRAM and video, and a separate on-chip peripheral bus to interface with low-speed peripherals such as serial ports, I²C, and GPIO. In the case of the 405LP, the former is called the Processor Local Bus (PLB) and the latter is known as the On-chip Peripheral Bus (OPB). The PCMCIA/CF controller hangs off the PLB, whereas the audio controller interface connects to the OPB.

An audio driver is built out of three main ingredients:

- Routines that handle playback
- Routines that handle capture
- Mixer control functions

Our driver implements playback, but does not support recording because the MP3 player in the example has no microphone. The driver also simplifies the mixer function. Rather than offering the full complement of volume controls, such as speaker, earphone, and line-out, it allows only a single generic volume control.

The register layout of the MP3 player's audio hardware shown in Table 13.1 mirrors these assumptions and simplifications, and does not conform to standards such as AC'97 alluded to earlier. So, the codec has a SAMPLING_RATE_REGISTER to configure the playback (digital-to-analog) sampling rate but no registers to set the capture (analog-to-digital) rate. The VOLUME_REGISTER configures a single global volume.

### Table 13.1. Register Layout of the Audio Hardware in Figure 13.4

| Register Name | Description |
|---|---|
| VOLUME_REGISTER | Controls the codec's global volume. |
| SAMPLING_RATE_REGISTER | Sets the codec's sampling rate for digital-to-analog conversion. |
| CLOCK_INPUT_REGISTER | Configures the codec's clock source, divisors, and so on. |
| CONTROL_REGISTER | Enables interrupts, configures interrupt cause (such as completion of a buffer transfer), resets hardware, enables/disables bus operation, and so on. |
| STATUS_REGISTER | Status of codec audio events. |
| DMA_ADDRESS_REGISTER | The example hardware supports a single DMA buffer descriptor. Real-world cards may support multiple descriptors and may have additional registers to hold parameters such as the descriptor that is currently being processed, the position of the current sample inside the buffer, and so on. DMA is performed to the buffers in the audio controller, so this register resides in the controller's memory space. |
| DMA_SIZE_REGISTER | Holds the size of the DMA transfer to/from the SoC. This register also resides inside the audio controller. |

Listing 13.1 is a skeletal ALSA audio driver for the MP3 player and liberally employs pseudocode (within comments) to cut out extraneous detail. ALSA is a sophisticated framework, and conforming audio drivers are usually several thousand lines long. Listing 13.1 gets you started only on your audio driver explorations. Continue your learning by falling back to the mighty Linux-Sound sources inside the top-level sound/ directory.

### Driver Methods and Structures

Our example driver is implemented as a platform driver. Let’s take a look at the steps performed by the platform driver’s probe() method, mycard_audio_probe(). We will digress a bit under each step to explain related concepts and important data structures that we encounter, and this will take us to other parts of the driver and help tie things together.

mycard_audio_probe() does the following:

- Creates an instance of a sound card by invoking snd_card_new():

```c
struct snd_card *card = snd_card_new(-1, id[dev->id], THIS_MODULE, 0);
```

The first argument to snd_card_new() is the card index (that identifies this card among multiple sound cards in the system), the second argument is the ID that’ll be stored in the id field of the returned snd_card structure, the third argument is the owner module, and the last argument is the size of a private data field that’ll be made available via the private_data field of the returned snd_card structure (usually to store chip-specific data such as interrupt levels and I/O addresses).

snd_card represents the created sound card and is defined as follows in include/sound/core.h:

```c
struct snd_card {
  int number;         /* Card index */
  char id[16];       /* Card ID */
  /* ... */
  struct module *module;   /* Owner module */
  void *private_data;      /* Private data */
  /* ... */
  struct list_head controls;
                    /* All controls for this card */
  struct device *dev;      /* Device assigned to this card */
  /* ... */
};
```

The remove() counterpart of the probe method, mycard_audio_remove(), releases the snd_card from the ALSA framework using snd_card_free().

- Creates a PCM playback instance and associates it with the card created in Step 1, using snd_pcm_new():

```c
int snd_pcm_new(struct snd_card *card, char *id,
                int device,
                int playback_count, int capture_count,
                struct snd_pcm **pcm);
```

The arguments are, respectively, the sound card instance created in Step 1, an identifier string, the device index, the number of supported playback streams, the number of supported capture streams (0 in our example), and a pointer to store the allocated PCM instance. The allocated PCM instance is defined as follows in include/sound/pcm.h:

```c
struct snd_pcm {
  struct snd_card *card; /* Associated snd_card */
  /* ... */
  struct snd_pcm_str streams[2]; /* Playback and capture streams of this PCM component. Each stream may support substreams if your h/w supports it */
  /* ... */
  struct device *dev; /* Associated hardware device */
};
```

The snd_device_new() routine lies at the core of snd_pcm_new() and other similar component instantiation functions. snd_device_new() ties a component and a set of operations with the associated snd_card (see Step 3).

- Connects playback operations with the PCM instance created in Step 2, by calling snd_pcm_set_ops(). The snd_pcm_ops structure specifies these operations for transferring PCM audio to the codec. Listing 13.1 accomplishes this as follows:

```c
/* Operators for the PCM playback stream */
static struct snd_pcm_ops mycard_playback_ops = {
  .open = mycard_pb_open, /* Open */
  .close = mycard_pb_close, /* Close */
  .ioctl = snd_pcm_lib_ioctl, /* Use to handle special commands, else specify the generic ioctl handler snd_pcm_lib_ioctl() */
  .hw_params = mycard_hw_params, /* Called when higher layers set hardware parameters such as audio format. DMA buffer allocation is also done from here */
  .hw_free = mycard_hw_free, /* Free resources allocated in mycard_hw_params() */
  .prepare = mycard_pb_prepare, /* Prepare to transfer the audio stream. Set audio format such as S16_LE (explained soon), enable interrupts, ... */
  .trigger = mycard_pb_trigger, /* Called when the PCM engine starts, stops, or pauses. The second argument specifies why it was called. This function cannot go to sleep */
};

/* Connect the operations with the PCM instance */
snd_pcm_set_ops(pcm, SNDRV_PCM_STREAM_PLAYBACK, &mycard_playback_ops);
```

In Listing 13.1, `mycard_pb_prepare()` configures the sampling rate into the `SAMPLING_RATE_REGISTER`, clock source into the `CLOCK_INPUT_REGISTER`, and transmit complete interrupt enablement into the `CONTROL_REGISTER`. The `trigger()` method, `mycard_pb_trigger()`, maps an audio buffer populated by the ALSA framework on-the-fly using `dma_map_single()`. (We discussed streaming DMA in Chapter 10, “Peripheral Component Interconnect.”) The mapped DMA buffer address is programmed into the `DMA_ADDRESS_REGISTER`. This register is part of the audio controller in the SoC, unlike the earlier registers that reside inside the codec. The audio controller forwards the DMA’ed data to the codec for playback.

Another related object is the `snd_pcm_hardware` structure, which announces the PCM component’s hardware capabilities. For our example device, this is defined in Listing 13.1 as follows:

```c
/* Hardware capabilities of the PCM playback stream */
static struct snd_pcm_hardware mycard_playback_stereo = {
    .info = (SNDRV_PCM_INFO_MMAP | SNDRV_PCM_INFO_PAUSE |
             SNDRV_PCM_INFO_RESUME); /* mmap() is supported. The stream has
                                       pause/resume capabilities */
    .formats = SNDRV_PCM_FMTBIT_S16_LE, /* Signed 16 bits per channel, little
                                         endian */
    .rates = SNDRV_PCM_RATE_8000_48000, /* DAC Sampling rate range */
    .rate_min = 8000, /* Minimum sampling rate */
    .rate_max = 48000, /* Maximum sampling rate */
    .channels_min = 2, /* Supports a left and a right channel */
    .channels_max = 2, /* Supports a left and a right channel */
    .buffer_bytes_max = 32768, /* Max buffer size */
};
```

This object is tied with the associated `snd_pcm` from the `open()` operator, `mycard_playback_open()`, using the PCM *runtime* instance. Each open PCM stream has a runtime object called `snd_pcm_runtime` that contains all information needed to manage that stream. This is a gigantic structure of software and hardware configurations defined in *include/sound/pcm.h* and contains `snd_pcm_hardware` as one of its component fields.

- Preallocates buffers using `snd_pcm_lib_preallocate_pages_for_all()`. DMA buffers are subsequently obtained from this preallocated area by `mycard_hw_params()` using `snd_pcm_lib_malloc_pages()` and stored in the PCM runtime instance alluded to in Step 3. `mycard_pb_trigger()` DMA-maps this buffer while starting a PCM operation and unmaps it while stopping the PCM operation.

- Associates a mixer control element with the sound card using `snd_ctl_add()` for global volume control:

```c
snd_ctl_add(card, snd_ctl_new1(&mycard_playback_vol, &myctl_private));
```

`snd_ctl_new1()` takes an `snd_kcontrol_new` structure as its first argument and returns a pointer to an `snd_kcontrol` structure. Listing 13.1 defines this as follows:
