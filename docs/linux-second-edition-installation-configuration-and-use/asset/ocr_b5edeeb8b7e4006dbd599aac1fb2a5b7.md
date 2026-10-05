# CONFIGURING THE X SERVER 227

Exceeding the frequency limits (in particular, the maximum line frequency) – which happens when the graphics cards supply too much data fast – may be dangerous. In such a case, the electron beam of the monitor can no longer follow the data, parts of the screen or even the whole screen are irradiated for too long and too intensively, and thus they overheat and for relatively short time (a matter of a few seconds) they are destroyed.

> CAUTION

Exceeding the maximum bandwidth is, however, quite (as long as the maximum line frequency is kept). The result is usually a smudged image, because the signal amplifier of the monitor is overloaded. For this reason, in more recent XFree6 configuration programs the bandwidth is no longer taken into account.

# The graphics card

The main task of the graphics card is to supply pixel data for image construction. (In addition, the card should support drawing operations – but this is not relevant here.) All current graphics cards can generate several graphic modes with different resolution and frequency – maybe even modes which your monitor might not be able to cope.

Frequencies play an important role for the graphics card as well. While the monitor must understand the data stream supplied at a pixel frequency, generation of this pixel frequency in the graphics card is a (technical) problem. Older graphics cards can only generate a few predefined frequencies, while modern cards are equipped with a freely programmable frequency generator. Frequencies provided by older graphics cards are an important element in the configuration of the video driver.

# Colors

Colors are no problem as far as the monitor is concerned. The monitor simply receives an analog value that reflects the intensity of a color component (red, green, blue). It is irrelevant whether 16 colors, 256 colors, or more are displayed.

For the graphics card, on the other hand, colors do constitute a problem: on the one hand, the greater the number of colors, the more data must be processed. An image with 256 colors takes twice the memory space of one with 16 colors. Modern graphics cards reach data streams up to 200 MBytes per second.

On the other hand, each digital pattern of a pixel may be converted into an analog signal. The digital/analog converters (DAC) are required for this purpose, however, work only up to a certain frequency. For many video cards, the DAC frequency is lower than the bandwidth theoretically supported by the card. Also, some graphics card manufacturers have to grown into a habit of changing the DAC chips all the time; for this reason, you must enter the precise denomination of the DAC chip into the configuration file for some graphics cards.

# Accelerator cards

These are graphics cards where the drawing operations are supported by a dedicated graphics chip. While with older cards the computer itself must make