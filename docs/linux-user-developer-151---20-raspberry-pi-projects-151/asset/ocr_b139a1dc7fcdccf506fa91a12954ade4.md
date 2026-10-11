![](bbox=[0.0, 0.0, 1.0, 0.3])

# Python column

for a particular language. But Pocket Sphinx is a research-level language system, so it has tools available to enable you to build your own models. In this way, you can train your code to understand your particular voice with all of its peculiarities and accents. This is a long process, so most people will not be interested in doing something so intensive. However, if you are interested, there is information available at the main website (cmusphinx.sourceforge.net). You can also define your own models and grammars to tell pocketsphinx how to interpret the audio that it is processing. Once again, effectively carrying out these tasks will require more in depth reading on your part.
If you want to process audio more directly, you can tell Pocket Sphinx to start processing with the function start _utt(). You can then start reading audio from your microphone. You will want to read in appropriate sized blocks of data before handing it in to pocketsphinx - specifically to the function process_raw() - and you will still need to use the function get_hyp() to actually get the translated text. Also, because your code can't know when someone has finished a complete utterance, you will need to do this from within a loop. On each pass of the loop, read another chunk of audio and feed it into pocketsphinx. You then need to call get_hyp() again to see if you can get anything intelligible from the data. When you are done doing this real-time processing, you can use the function end_utt().
So far, we have covered how to record your speech and how to turn that speech into text. In the next issue, you will learn how to take that translated speech and actually take actions based on how the system has been configured. But even with only these two steps, you could build yourself a nifty little dictaphone or vocal note-taking system.

# Full code listing

```
# Your first need to import the required modules
import pocketsphinx as ps
import sphinxbase

# Next, you need to create a Decoder object
hmmd = '/usr/share/pocketsphinx/model/hmm/en_us' lmd = '/usr/share/pocketsphinx/lm/ws/j/wlist50_3e-7.vp.tg.lm.DMP' dictd = '/usr/share/pocketsphinx/lm/ws/j/wlist50.dic'
d = ps.Decoder(hmm=hmmd, lmd=lmd, dict=dctd)

# You need to jump over the header information in your WAV file
wavFile = file('my_file.wav', 'rb')
wavFile.seek(44)

# Now you can decode the audio
d.decode_raw(wavFile)
results = d.get_hyp()

# The most likely result is the first one
decoded_speech = results[0]
print( I said ", decoded_speech[0], " with a confidence of ", decoded_speech[1]

# To do live decoding, you need the PyAudio module
import pyaudio
p = pyaudio.PyAudio()

# You can now open an input stream
in_stream = p.open(format=pyaudio.paInt16, channels=1, rate=16000, input=True, frames_per_buffer=1024)
in_stream.start_stream()

# Now you can start decoding
d.start_utt()
while True:
buf = in_stream.read(1024)
d.process_raw(buf, False, False)
results = d.get_hyp()
# Here you would do something based on the decoded speech
# When you are done, you can shut everything down
break
d.end_utt()
```