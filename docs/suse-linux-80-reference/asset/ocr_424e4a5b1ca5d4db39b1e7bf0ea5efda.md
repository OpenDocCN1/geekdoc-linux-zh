# Main PCM Types: hw and plughw

ALSA 0.9.x has changed and extended the concept of PCM devices. From now on, by selecting a given PCM type, the user can influence how ALSA accesses the sound card. The most important PCM types are hw and plughw.

To understand the difference between the two types, it is necessary to know how a PCM device is opened. Setting (at least) the following parameters is required: sample format, sample frequency, number of channels, number of periods (previously referred to as “fragments”), and size of a period. For example, an application may want to play back a WAV file with a sample frequency of 44.1 kHz, but the sound card does not support this frequency. In this case, ALSA automatically converts the data in the plug-in layer to a format the sound card supports. The conversion affects the parameters sample format, sample frequency, and number of channels.

Selecting the PCM type plughw activates the plug-in layer. Selecting the PCM type hw causes ALSA to attempt to open the PCM devices directly with the parameters required by the application.

The complete designator for a PCM device consists of the PCM type followed by a colon then the card number followed by the device number, for example:

`plughw:0,0`