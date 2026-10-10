can search for people who might be connected to Elgiga server by first name, last name, e-mail address, or location. Select a person from the list that appears and, if he or she accepts your call, you can begin videoconferencing. The History tab shows a log of your activities.

# # Playing Video

Video recording (encoding) and playback (decoding) remain among the most contentious areas of potential litigation in Open Source software. On one hand, you have patent holders of complex video formats that might ask for royalties for Open Source codecs (even when the software was written from “scratch”). On the other hand, you have the movie industry, which has taken aim at those publishing what they had hoped were secret encryption techniques (DeCSS), to prevent the Open Source decoding of commerical movies. The problem is that the same technique that allows you to play movies in Linux also can be used to copy and share them.

> > **NOTE** Codec stands for Coder/Decoder or Compressor/DECompressor, depending on whom you ask. In either case, codecs are what make it possible to process and encode audio and video on computers.

As with audio recording, if you are starting from scratch, there is an Open Source codec called Theora (www.theora.org) that you can use without paying any royalties. As of this writing, Provided you own the content you are recording, you can freely distribute that content as well and allow others to play it back. (See the sidebar “Converting Video to Theora” for details.)

When it comes to including video codecs (other than the free Theora), CentOS has taken the cautious approach. While CentOS now includes video players such as Totem (described later in this chapter), it does not include players (such as the MPlayer and Xine media players) that often are packaged with contentious codecs. If you want to play commercial movies, popular video clips, or other video content in a CentOS system, you have to get those codecs elsewhere.

This section describes some of the issues surrounding playing and creating videos in Linux. It also describes video players that come with CentOS, as well as those you can obtain to play a wide variety of video content.

# ## Examining Laws Affecting Video and Linux

I need to start out by reminding everyone that I am not a lawyer, so you need to take responsibility yourself regarding any software you put on your computers. However, there are several themes that have arisen in regard to playing video content with Open Source software in Linux:

+   * Licensing fees for patented codecs may be required. While many video codecs are covered by patents, some patent holders don’t charge for personal use. However, you should check current policies of companies who own patents on codecs you plan to use, as the terms of use are constantly changing. For example, this statement that was once posted on the DivX