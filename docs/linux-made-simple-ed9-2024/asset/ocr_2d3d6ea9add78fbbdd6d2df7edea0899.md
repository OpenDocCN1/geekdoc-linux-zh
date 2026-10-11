# # Rhythmbox: Playing media

Get your music collection blasting from your speakers and super-organised, then watch some videos too.

Remember the days when we used to buy CD players with built-in radios, or cassette tapes for listening to our music? No? You’re not alone. When it’s possible to carry around a lifetime’s worth of tunes on your phone, and stream audio wirelessly to your TV or HiFi system wirelessly, why on Earth would you invest in something so archaic?

We’ll wager everyone needs a good media player on their desktop, however. Whether it’s to enjoy music or internet radio while you work, or watch a movie on your laptop while travelling by train, digital media should be enjoyable whenever, wherever and however you need it.

And fortunately, Ubuntu has all the tools you need for playback built-in. If you’re coming from Windows, there is one key adjustment you’ll have to make. Microsoft’s operating system comes with the all-encompassing *Windows Media Player* built-in, which is a hub for both music and video played back from a local source – like a hard drive or USB key – or a networked drive. For entertainment purposes, Ubuntu has separate applications for video and music playback.

For music, that application is *Rhythmbox*, which can manage your audio library, stream from remote services or a household server, and rip CDs directly to your hard drive. For video, the *Totem* player – which appears in the Unity launcher under the name *Videos* – serves similar purposes.

# ## Living in a Rhythmbox

As far as audio goes, *Rhythmbox* is as fully featured as you need. It can be used to playback music from a local library, rip CDs, add album art to digital files automatically, purchase songs online and stream from another PC or network attached storage.

Before you start using *Rhythmbox*, however, there’s one important thing you’ll need to bear in mind. By default, Ubuntu doesn’t include the software codecs required to playback the common MP3 format which many people use to store songs digitally. Because many parts of the MP3 codec are still protected by patents, Linux distributions are unable to include it as standard without paying a licence fee.

Fortunately, the way around this is simple. Open up the *Ubuntu Software Centre* and search for “*Ubuntu Restricted Extras*”. If it’s not installed yet, click for download and there’s little your PC will left unable to play.

Back to *Rhythmbox*, the first time you open it up you’ll want to point it at the place where you keep your song files stored in order to build up its library list. Open up the Edit menu and click *Preferences*, then *Music*. Click the *Browse* button to direct *Rhythmbox* to your Music library folder if it’s not the default one, and then put a tick in the box “*Watch my library for new files*”. Now any songs and albums in your library will be added to the *Rhythmbox* home screen, and any time you rip a CD, purchase music through *Rhythmbox* or add music from a portable player it’ll be saved to the same physical place.

You’ll also see options on this screen to select the format and quality for ripping music, and also for the naming convention you prefer in filenames that are automatically generated.

Once you’ve loaded some music up, the main view for *Rhythmbox* is fairly straightforward (see boxout above). You’ll notice that the column on far left is pretty sparse initially, with some basic library options for selecting music, podcasts (see boxout) or internet radio stations. You can also see what’s coming up in the play queue.

To start adding extra options here, you’ll need to visit the *Plugins* menu, which you’ll find if you click on *Tools* in the menu bar.

*Rhythmbox* comes with extra features which are disabled by default. In this menu you can turn extras such as Last FM scrobbling and the Jamendo music store. The selection of plugins is fairly limited initially, but you can add more with ease.

The one essential plugin to install is the *Gnuio suite*, which will enable you to stream from other computers and libraries on your network. If *Gnuio* isn’t already installed, open up the *Software Centre* and search for gnuio-plugins, then install the *Base package* from there. Enabling this in the *Rhythmbox Plugins* section should result in any shared libraries on your network popping up in the left-hand menu.

> **Quick tip**
> 
> When it comes to online music, there’s a desktop client for Spotify that can be added to Ubuntu and Google Play Music works through the browser. Netflix can be accessed if you install the Chrome browser, or use the User Agent Override add-on in Firefox.

![](bbox=[0.09, 0.67, 0.54, 0.85])

> Probably the best Ubuntu video player, VLC is a must-have install.