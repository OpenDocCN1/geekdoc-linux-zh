# Use Python with Pi

# Voice synthesizer

# What you'll need...

Portable USB speakers python-espeak module eSpeak Raspbian (latest edition)

# Voice synthesizer
Add the power of speech to your Raspberry Pi projects with the versatile eSpeak Python library

We've shown how the Raspberry Pi can be used to power all kinds of projects, but as a tiny computer it can also be the centre of Internet of things in your house. For these reasons and more, using the Raspberry Pi for text-to-voice commands could be just what you're looking for. Due to the Debian base of Raspberry, the powerful eSpeak library is easily available for anyone looking to make use of it. There's also a module that allows you to use eSpeak in Python, going beyond the standard command-line prompts to perform automation tasks.

> Did you know...
Using eSpeak can control the way words are spoken to add emphasis or make the sound different.

![](bbox=[0.052, 0.516, 0.318, 0.755])

# Pi's first words

The eSpeak library is pretty simple to use – to get it just saying something, in the terminal:

```
$ eSpeak "[message]"
```

This will use the library's defaults to read whatever is written in the message, with decent clarity. Though this simple command is fun, there's much more you can do...

# Say some more

You can easily read text with many different options, such as gender, read speed and even when it pronounces syllables. For example, writing the command like:

```
$ eSpeak -venf3 -k5 -s150 "[message]"
```

...will turn the voice female, emphasise capital letters and make the reading slower.

# Everything you'll need

+   01 We'll install everything we plan to use in this tutorial at once.
This includes the eSpeak library and the Python modules we need to show off. Open the terminal and install with:

```
$ sudo apt-get install espeak python-espeak python-tk
```