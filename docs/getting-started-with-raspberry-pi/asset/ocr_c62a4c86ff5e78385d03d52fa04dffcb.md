| Kernel Interface | Location | Description |
| :--- | :--- | :--- |
| snd_card_register() | sound/core/init.c | Registers a sound card with the ALSA framework |
| snd_pcm_lib_preallocate_pages_for_all() | sound/core/pcm_memory.c | Preallocates buffers for a sound card |
| snd_pcm_lib_malloc_pages() | sound/core/pcm_memory.c | Allocates DMA buffers for a sound card |
| snd_pcm_new() | sound/core/pcm.c | Creates an instance of a PCM object |
| snd_pcm_set_ops() | sound/core/pcm_lib.c | Connects playback or capture operations with a PCM object |
| snd_ctl_add() | sound/core/control.c | Associates a mixer control element with a sound card |
| snd_ctl_new1() | sound/core/control.c | Allocates an snd_kcontrol structure and initializes it with supplied control operations |
| snd_card_proc_new() | sound/core/info.c | Creates a /proc entry and assigns it to a card instance |