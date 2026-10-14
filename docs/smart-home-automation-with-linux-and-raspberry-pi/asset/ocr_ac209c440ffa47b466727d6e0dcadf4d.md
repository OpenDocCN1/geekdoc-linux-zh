You will notice that playback always takes an array of sample data, rather than a filename. If you have a shield which lets you work with an SD card, or USB memory stick, then you can fashion playback from a file. Without it, however, you need to access it directly as raw data that involves processing the audio file offline, and producing a large array that can be read as such.

There are various code solutions to the problem of generating this array, although the output is nothing more than the 8-bit output levels of each sample in the sound. Typical packages include EncodeAudio (https://github.com/damellis/EncodeAudio) and wav2c, mplayer, and sox.

The limitations of this method are many but, on an unshielded Arduino, what do you expect? Primarily, you need to store the data in its Flash memory (not RAM) that takes away from your program space. But still, you are limited to around 4 seconds of audio, in 8-bit, sampled at 8KHz.

To surpass these limitations you need two things: more memory, and a custom chip capable of faster playback. Fortunately, these problems go hand-in-hand, as you need a shield that supports external flash memory to handle the former, so makers of the latter have included it for free. The two workhorses in this area are the Sparkfun MP3 Player shield (https://www.sparkfun.com/products/10628) and Lady Ada’s wave shield (http://www.ladyada.net/make/waveshield/) which provides playback support for .wav files, up to 16-bit mono 22KHz samples, which is a marked improvement over the PCM examples we saw earlier. It also provides a small power amplifier, able to drive 1/8W 8 ohm speakers. This could be used for a talking clock, a kitchen-based stopwatch, or a virtual pet.

Before planning any projects however, you need to carefully consult the specification of the hardware since the software libraries necessary for this task can be very large (because they include Flash access, as well as sample playback—the wave shield for example uses 10KB of memory) so you might not have room for all of your automation control logic. Or you might need to upgrade to a better chip.

> **Note**  The filesystem on Arduino-accessible flash memory generally uses 8.3 filenames, so it is not possible to prec or d speed for every word from the dictionary without an additional lookup table.

# Display systems

If you need a full display, or high resolution graphics, then your Arduino will probably have to concede defeat to the Raspberry Pi. However, for many applications, this isn’t necessary.

The simplest form of display to connect is an LCD, such as the SparkFun SerLCD (https://www.sparkfun.com/products/9393) that provides two lines of 16 characters, along with a back light. Such devices require no additional driver hardware, and the LCD library is provided as standard. The font is also held in the device, so messages can be display simply with

```
```cpp
// initialize the library with the numbers of the interface pins
LiquidCrystal lcd(12, 11, 5, 4, 3, 2);

lcd.begin(16, 2);
lcd.print("hello, world!");
```
```

This is normally enough for warnings and basic messages, although you can always buffer and scroll messages along if need be.

If wiring is more interesting to you, then it is also possible to drive several LED matrix devices from a single Arduino, like this example http://g33k.blogspot.co.uk/2010/02/arduino-56x8-scrolling-led-matrix.html. This has the benefit of having per-LED control, and still be fairly low power. The next step up from here is to use a TV display, which the Arduino is capable of driving directly through the composite socket!