# Audio effects

# # PauXStretch

If you're into music production, or otherwise playing around with audio, time stretching is one of the most common audio effects you can use. This is because time stretching is both practical and creative. It's practical because it enables you to mix audio recorded at one speed with audio recorded at another, without any sign that the audio has been processed. It's creative because your audio becomes malleable in both duration and pitch. Both time stretching and pitch shifting are intrinsically linked because, to make a duration longer or shorter, audio is slowed down or speeded up. This affects its pitch. And the process to restore pitch isn't easily accomplished. The human voice, for example, contains formants that don't track the fundamental pitch of the voice. They need to be filtered out and separately processed, and there are the same caveats for any other type of

music, instrumentation, or percussion.

To accommodate all this audio complexity, all kinds of algorithmic dealings have been created for dealing with specific types of sound, and many of those techniques can also be used creatively. Which is exactly what this audio plugin, PauXStretch, has been designed to do. The Paul in its name comes from the central algorithm it uses to process audio (Paul's Extreme Time Stretch, originally developed by Nasca Octavian Paul), but the plugin has been designed to give you quick and easy access to a comprehensive suite of time stretching related functions that can do anything from accurately changing the pitch of your audio to mangled it beyond all recognition. There are seven horizontal modules that can be selectively enabled or disabled, and these manipulate the stretch amount, harmonics, noise, frequency shift and spread, a

![](bbox=[0.54, 0.08, 0.92, 0.34])

Alongside the pitch and time shifting, there are some excellent standard effects that can be used in isolation, including compression and equalization.

low- and high-pass filter, and even binaural processing. Their order can be changed with a flow diagram below the module parameters. Beneath this is a tabbed view to show the sampled audio waveform, the processed segment ratios, and an equalizer.

This might all sound complicated, but you can easily play with the controls without understanding their function, and the sound can range from slight tonal differences to huge, glitching feedback loops. You can either process a file or an incoming stream and send the output back to your audio application or to an exported file. Audio can be sampled and frozen, with a subsection selected from the waveform view for special tasks. It works well as a DJ or musician's effect for real-time processing, and it's equally adept as a drop-in effect in Ardour or Bibitub. But what's especially remarkable about this plugin is its quality, and that could be because its developer usually makes commercial and proprietary open source audio and can even be built as a shiny new and unexplored CLAP plugin (which is how we tested it). The UI has a level of professionalism you don't often see in open source plugins. While there are many different options crammed into its single window, they're easy to navigate and don't overwhelm the UI with complexity. This is a genuine accomplishment that's quite apart from the amazing sound processing the plugin is capable of, and it's brilliant to see effects like these making their way to Linux.

![](bbox=[0.07, 0.6, 0.52, 0.9])

PauXStretch is one of the first audio plugins we've been able to build and use as a CLAP plugin, making it ideal for powerful Linux audio processing and manipulation.

Project Website
https://github.com/essej/pauxstretch