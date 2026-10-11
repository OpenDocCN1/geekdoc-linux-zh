
# Make a Raspberry Pi sampler

**Build your own looping drum machine with only 200 lines of code!**

![](img/a1548a579bd09ff29b2b92de3f565e63_115_0.png)

*Left: Extra breadboards are used here to keep the main breadboard as free from wires as possible*

## What you'll need

- Latest Raspbian image (raspberry pi.org/downloads)
- At least one breadboard
- Push buttons
- LEDs
- Female-to-male GPIO jumper cables
- Male-to-male GPIO jumper cables

In this tutorial we combine electronics, music and programming knowledge to create a simple sampler with looping capabilities. The implementation used in this article has three drum sounds as the samples, but it is trivial to add more until you run out of GPIO pins.

Before we start, I'll cover some basic musical terms. Music is split into bars. There are a certain number of beats in a bar. This sampler uses the 4/4 time signature, which means there are 4 beats in each bar. Tempo is the speed at which music is played, and it is measured in beats per minute (bpm). A metronome is an audible tone that is heard at the start of every beat.

Quantization is the process of aligning notes to beats, or exact fractions of a beat, and a quantization value is usually given in the form 1/8. This means that there are eight possible places in a bar where a note can be played. When the sampler is recording and a sample button is pressed, we store the sample at the current position in the bar with the accuracy of the quantize value. There's a lot to cover, so let's get started.

## 01 Connect LEDs

The circuit diagram is an LED that can be turned on and off with a GPIO output. The orange wire is the connection from the GPIO output. This then goes through a 220Ω resistor to limit the current draw to a safe level. This current flows through the positive leg of the LED and then back to ground. We need nine LEDs for this project.

![](img/a1548a579bd09ff29b2b92de3f565e63_115_1.png)

## 02 Wire up buttons

The second circuit we need is a push button. The purple wire goes to a GPIO input. There is a 10KΩ pull down resistor to ground, which represents a logical 0. When the push button is pressed, the 3.3V supply representing a logical 1 is connected to the purple wire. The electricity takes this path because it has less resistance than the path to ground. We need two buttons for record and undo, and then as many buttons as you like for samples (three drum samples are provided).

## 03 Download samples

Create a folder for the project called pismsampler. Then download and unzip the sounds:

```bash
mkdir pismsampler
cd pismsampler
wget http://liamfraser.co.uk/Lud/pismsampler/sounds.zip
unzip sounds.zip
```

There will now be a folder called sounds with some samples in. The file format for samples is .wav audio, Mono/PCM, 16 bit, stereo, 44100 Hz. Mono will work too. Any samples can be converted to this format with Audacity by exporting them as a .wav file.

## 04 Import required libraries

Create a file called pismsampler.py in your favourite editor. The first thing we need to do is import the required libraries and set some configuration values. A key option is debounce; the time to wait before a button can be pressed again to stop accidental presses from contact bounce.

## 05 Create a sample class

We're going to use a class to represent each sample. It's going to need a few things: the pin that the sample button is connected to, the name of the sound file, and a reference to the instance of the sampler class. We haven't created the sampler class yet, but the sample will need to be able to tell if the sampler is recording or not, and have access to the data structure that recordings are stored in to add itself to if necessary.

The other thing that we need to do is set the GPIO pin to an input, and add an event listener for when the button is pressed. We set callback (the function to be executed when the button is pressed) to a function called self.play_btn, which will play a sound and add it to the recording data if we are recording. It will become abundantly clear how this works once we've written the sampler class. Note that the GPIO event handler passes the pin that the event handler was triggered on, hence the channel variable that is present but never used.

### Full code listing

```python
import RPi.GPIO as GPIO
import time
import pygame
import os

beat_leds = [2, 3, 4, 17]
bar_leds = [27, 22, 18, 9]
record_led = 11
record = 19
undo = 26
debounce = 200 # ms

class Sample(object):
    def __init__(self, pin, sound, sampler):
        self.sampler = sampler
        self.name = sound
        self.sound = pygame.mixer.Sound(os.path.join('sounds', sound))
        self.pin = pin
        GPIO.setup(pin, GPIO.IN)
        GPIO.add_event_detect(self.pin, GPIO.RISING, callback=self.play_btn, bouncetime=debounce)

    def play_btn(self, channel):
        self.sound.play()
        s = self.sampler
        if s.recording:
            s.recording.data[s.bar_n][s.quantize_n].append(('loop': s.loop_count, 'sample': self))

class PiSampler(object):
    def __init__(self, tempo=80, quantize=16):
        pygame.mixer.pre_init(44100, -16, 1, 512)
        pygame.init()
        
        self.quantize = quantize
        self.tempo = tempo
        self.recording = False
        self.record_next = False
        
        self.metroone = False
        self.met_low = pygame.mixer.Sound(os.path.join('sounds', 'met_low.wav'))
        self.met_high = pygame.mixer.Sound(os.path.join('sounds', 'met_high.wav'))
        self.met_low.set_volume(0.4)
        self.met_high.set_volume(0.4)
        
        self.samples = []
        
        self.recording_data = []
        for i in range(4):
            bar_arr = []
            for j in range(4, quantize):
                bar_arr.append([])
            self.recording_data.append(bar_arr)

        GPIO.setmode(GPIO.BCM)
        for pin in beat_leds + bar_leds + [record_led]:
            GPIO.setup(pin, GPIO.OUT)

        GPIO.setup(record, GPIO.IN)
        GPIO.add_event_detect(record, GPIO.RISING, callback=self.record_next_loop, bouncetime=debounce)
        GPIO.setup(undo, GPIO.IN)
        GPIO.add_event_detect(undo, GPIO.RISING, callback=self.undo_previous_loop, bouncetime=debounce)

    @property
    def tempo(self):
        return self._tempo

    @tempo.setter
    def tempo(self, tempo):
        self._tempo = tempo
        self.seconds_per_beat = 60.0 / tempo
        
        self.quantize_per_beat = self.quantize / 4
        self.quantize_seconds = self.seconds_per_beat / self.quantize_per_beat

    def add(self, sample):
        self.samples.append(sample)

    @property
    def recording(self):
        return self._recording

    @recording.setter
    def recording(self, value):
        self._recording = value
        GPIO.output(record_led, value)

    def record_next_loop(self, channel):
        self.record_next = True

    def play_recording(self):
        for sample_dict in self.recording_data[self.bar_n][self.quantize_n]:
            if sample_dict['loop'] != self.loop_count:
                sample_dict['sample'].sound.play()

    def undo_previous_loop(self, channel):
        if len(self.last_recorded_loop) == 0:
            print "No previous loop to undo"
            return

        print "Undoing previous loop"

        loop = self.last_recorded_loop.pop()

        for bar in self.recording_data:
            for quantize in bar:
                removes = []
                for sample in quantize:
                    if sample['loop'] == loop:
                        removes.append(sample)
                for sample in removes:
                    quantize.remove(sample)

    def do_leds(self, leds, n):
        count = 0
        for led in leds:
            if count == n:
                GPIO.output(led, True)
            else:
                pass
            count += 1
```

## 06 The sampler init method

Here's the start of the sampler class. The last value in the Pygame mixer init is the buffer size. You might need to increase this to 1024 or higher if you have audio dropouts. We create some variables to store recording data. Metronome sounds are then added and their volume lowered. We also create a list to hold our samples in.

We create nested arrays to represent recorded sample presses. There is an array for each bar. Each bar has an array for each possible quantize value. The default value of 64 gives us 64 possible places to store a sample hit per bar.

Finally, we set up the LED pins, and the pins for the record and undo buttons.

## 07 The tempo property

The tempo variable is actually a property with a custom setter. This means when a value is assigned, it does a custom action. In our case, we need to calculate how often we need to check for recorded notes to play in the main loop that we'll write later.

## 08 Helper functions

There are a few helper functions in the class. One of them simply adds a sample to the list of samples. Another sets a variable to trigger recording at the start of the next loop. There is also a function which turns the red LED on when the recording variable is set to true. Now we'll jump forward and take care of the main loop towards the end of the full code listing.

## 09 Start the main loop

The main loop doesn't actually have to do any work at all to play sounds, as that's done by the GPIO event handlers. The main loop is used to play the metronome, update the state about which bar/beat/quantize we are currently on, update the LEDs and deal with recording if necessary.

Before the loop, we create variables to track the state. The last recorded loop is a list that we will use as a stack. A stack is a last in/first out data structure, allowing us to undo recordings multiple times by removing each sample that was recorded when the loop count was the value on the top of the stack.

If we're at the start of a new beat then we use a function called do_leds that we haven't created yet. As the LEDs work in the same way (a block of four LEDs where only one is turned on), we can use the same function twice and just pass a different set of pins, and the index of the LED we want to turn on. We then call the do_metronome function which will play the appropriate metronome sound.

We then do some recording logic which starts recording if we should be recording, and stops recording if we have just been recording, adding the
