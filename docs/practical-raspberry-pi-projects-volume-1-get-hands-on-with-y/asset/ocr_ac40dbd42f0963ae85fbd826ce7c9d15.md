![](bbox=[0.0, 0.12, 0.98, 0.54])

> It's easier to make your Raspberry Pi talk than you might think, thanks to eSpeak

# # Raspberry Pi voice synthesizer
**Add the power of speech to your Raspberry Pi projects with the versatile eSpeak Python library**

+   **What you'll need**
+   
+   - Portable USB speakers
+   - python-espeak module
+   - eSpeak
+   - Raspbian (latest image)

We've shown in previous issues how the Raspberry Pi can be used to power robots, and as a tiny computer it can also be the centre of an Internet of Things in your house or office.

For these reasons and more, using the Raspberry Pi for text-to-voice commands could be just what you're looking for. Due to the Debian base of Raspbian, the powerful eSpeak library is easily available for anyone looking to make use of it. There's also a module that allows you to use eSpeak in Python, going beyond the standard command-line prompts so you can perform automation tasks.

![](bbox=[0.55, 0.72, 0.88, 0.84])

# **01 Everything you'll need**

We'll install everything we plan to use in this tutorial at once. This includes the eSpeak library and the Python modules we need to show it off. Open the terminal and install with:

```
`$ sudo apt-get install espeak python-espeak python-tk`
```