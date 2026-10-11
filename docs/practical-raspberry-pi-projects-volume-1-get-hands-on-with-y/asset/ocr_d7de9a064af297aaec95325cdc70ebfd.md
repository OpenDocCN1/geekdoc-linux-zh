# Full code listing (Cont.)

```
```python
return out_sample

class Synth:
    BUFSIZE = 1024
    SAMPLE_RATE = 44100

    def __init__(self):
        self.audio = pyaudio.PyAudio()

        # Create output buffers
        self.buf_a = array('h', [0] * Synth.BUFSIZE)
        self.buf_b = array('h', [0] * Synth.BUFSIZE)
        # Oldbuf and curbuf are references to buf_a or buf_b, not copies. We're filling newbuf
        # while playbuf is playing
        self.playbuf = self.buf_b
        self.newbuf = self.buf_a

        self.load_wavetable()

        self.notes = []
        self.notes_on = []

        # The synth loop will run in a separate thread.
        # We will use this condition to notify it when
        # we need more samples

        self.more_samples = threading.Event()
        self.exit = threading.Event()

        # MIDI table of note -> frequencies
        self.midi_table = MIDITable()

    def stop(self):
        print("Exiting")
        self.exit.set()
        self.stream.stop_stream()
        self.stream.close()

    def stream_init(self):
        self.stream = self.audio.open(
            format=pyaudio.paInt16,
            channels=1,
            rate=Synth.SAMPLE_RATE,
            output=True,
            frames_per_buffer=Synth.BUFSIZE,
            stream_callback=self.callback)

    def load_wavetable(self):
        # Load wavetable and assert it's the
        # correct format
        fh = wave.open('square.wav', 'r')
        assert fh.getnchannels() == 1
        assert fh.get framerate() == Synth.SAMPLE_RATE
        assert fh.getsampwidth() == 2  # aka 16 bits

        # Read the wavdata as a byte string. Then
        # need to convert this into a sample array we
        # can access with indexes

        data = fh.readframes(fh.getnframes())

        # h is signed short, or int16_t
        self.wavetable = array('h')
        self.wavetable.fromstring(data)

    def swap_buffers(self):
        tmp = self.playbuf
        self.playbuf = self.newbuf
        self.newbuf = tmp
        # Setting the condition makes the synth loop
```
```text
Step 09
```
```

# CODE A SIMPLE SYNTHESISER

# Synthesis theory

Wavetable synthesis is where you use a single cycle of a wave as a lookup table to synthesise sound. In this case we have a squarewave, but you can load any wave shape you like. CD-quality audio has a sample rate of 44.1kHz, which is what we used in our implementation. At each sample, the synthesiser outputs a value from the wavetable and then increments a position pointer to the next value in the table. However, if the wavetable has a frequency of 440 Hz then we need to be able to step through it at arbitrary sizes (ie non-integer values). To achieve this, we use linear interpolation. Assuming the table had a frequency of 440 Hz and we wanted a frequency of 220 Hz, we'd need to step through the table at a step size of 0.5. This can be thought of as drawing a line between two values in the table and picking a value on the line as your output. As an example, if element 0 is 8 and element 1 is 10 then element 0.5 would be 5 + (10-5) × 0.5, which gives us a value of 7.5. When you reach a position that goes over the end of the table, you wrap around and start again. There is no discontinuity as we're storing a single cycle of the wave in the table. The equation for step size is:

```
```
step_size = table_size * (note_frequency / sample_rate)
```
```

The wavetable oscillator gets us noise at the desired frequency, but it's always at maximum amplitude and will sound rough and unnatural. If you cut off a wave in the middle of a cycle there will be a pop or click, so this is where Attack, Decay, Sustain and Release envelopes help. These change the amplitude of the raw oscillator output over time to sound more like an instrument. This is done by applying a fractional multiplier to the original sample point returned by the wave table oscillator. Having a release time from 100% volume to 0% means that a note will fade out smoothly, when it's turned off. With the right ADSR curves and the correct wavetable, a synthesiser can sound very similar to real instruments.

More information can be found at: bit.ly/1KgDgp.

![](bbox=[0.6, 0.67, 0.95, 0.91])

Above here's one cycle of a wavetable oscillator