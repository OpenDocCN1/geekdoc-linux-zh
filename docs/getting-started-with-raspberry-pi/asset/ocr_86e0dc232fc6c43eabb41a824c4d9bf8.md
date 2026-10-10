```
{
    /* Enable Transmit DMA complete interrupt by writing to
    CONTROL_REGISTER using codec_write_reg() */

    /* Set the sampling rate by writing to SAMPILING_RATE_REGISTER */

    /* Configure clock source and enable clocking by writing
       to CLOCK_INPUT_REGISTER */

    /* Allocate DMA descriptors for audio transfer */

    return 0;
}

/* Audio trigger/stop/.. */
static int
mycard_pb_trigger(struct snd_pcm_substream *substream, int cmd)
{
    switch (cmd) {
    case SNDRV_PCM_TRIGGER_START:
        /* Map the audio substream's runtime audio buffer (which is an
           offset into runtime->dma_area) using dma_map_single(),
           populate the resulting address to the audio controller's
           DMA_ADDRESS_REGISTER, and perform DMA */
        /* ... */
        break;

    case SNDRV_PCM_TRIGGER_STOP:
        /* Shut the stream. Unmap DMA buffer using dma_unmap_single() */
        /* ... */
        break;

    default:
        return -EINVAL;
        break;
    }

    return 0;
}

/* Allocate DMA buffers using memory preallocated for DMA from the
   probe() method. dma_[map|unmap]_single() operate on this area
   later on */
static int
mycard_hw_params(struct snd_pcm_substream *substream,
          struct snd_pcm_hw_params *hw_params)
{
    /* Use preallocated memory from mycard_audio_probe() to
       satisfy this memory request */
    return snd_pcm_lib_malloc_pages(substream,
                                    params_buffer_bytes(hw_params));
}

/* Reverse of mycard_hw_params() */
static int
mycard_hw_free(struct snd_pcm_substream *substream)
{
    return snd_pcm_lib_free_pages(substream);
}
```