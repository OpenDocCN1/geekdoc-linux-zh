
## The other half of WordPress

The story of WordPress co-founder, Mark Little

![](img/dd9251551a61a36067892b1cc68615b0_54_0.png)

not sold and yes, I continued in my day job. Matt went to work for CNET, which had just started using WordPress for just a couple of things, and they actually had him doing a standard software development job. But they paid for him to work one day a week on WordPress itself and I think it was through working there that he met a guy called Tony Schneider, who had just sold some software to Yahoo! for £25m or something like. Matt had started Autonomic at this point. Schneider later managed to help raise funding for him and joined the service that eventually became WordPress.com. But me, I continued in my day job up until 2008.”

### Carrying on

Little considered becoming part of WordPress.com, which is a blog web hosting service provider owned by Autonomic, but this was prior to the funding and the company couldn’t afford to pay him a wage. “Today it is financially supported via paid upgrades, VIP services and advertising and pay pages, but in the early days there wasn’t much cash for this and the bulk of the fund-raising efforts went on infrastructure.”

**4 billion**
The number of page views of WordPress websites from April 2012 to April 2013

Up until the first release, the development team consisted of just Mullenweg and Little, but five people were working on the project after that by the end of 2003 and it continued to grow after that. By the end of 2005, Little wasn’t able to stay involved. “I had issues at home, real-life issues which meant that I couldn’t spend the time working on this thing voluntarily,” he says. “It was still a very techy thing, a very geek thing, it wasn’t as good and as user-friendly as it has become today and it certainly wasn’t as prominent.”

Cash, he insists, is something that does not motivate him, however. “I need to pay the bills and we need to eat,” he says. “I am the breadwinner of the house and I always have been, but I wish I could put that side of things in place and do what interests me from that point on. There’s no doubting my passion for open source computing.”

Indeed, he has read up on the philosophy behind the General Public’s License and he has devoured Richard Stallman’s story of how he created the free software movement. “I not only found it very inspiring,” he says, “it just seemed the morally right thing to do, for me. The fact is that, at the time, in the 1970s and 1980s, software companies were effectively creating artificial scarcity, based on intellectual ideas that were almost free to reproduce. Back then firms were making floppy disks and putting them in boxes and getting manuals printed and they were charging £500 or £600 for a product that had just £30 or £40 worth of materials. As things moved on, it got easier and easier to distribute software online where the distribution costs and the reproduction costs approach zero, so to then charge artificial amounts on top of that just seemed like the wrong thing to do.”

He hopes that future generations go down the same path and release open source software. “But first, he says, “I think it is crucial that we just get kids learning how to code. There are some good moves in that direction and I love what is being done with the Raspberry Pi. Suddenly, a school can’t say it can’t afford to buy lots of computers to experiment with. These are costing £25 each, it’s a great time to be in computing and I feel it’s good to be plugging back in and helping people learn.”

Mike Little’s new website is at **mikelittle.org** but he also runs his company site, **zed1.com**.

## OUTSTANDING CONTRIBUTION TO DIGITAL

At SASCon 2013, Mike Little was presented with the inaugural ‘Outstanding Contribution to Digital’ award for his part in co-founding and developing WordPress.

The award, which was handed out at a conference at the new Manchester Metropolitan University Business School, acknowledged his instrumental role in setting up and developing the first version of WordPress, which has become the most popular content management system on the internet.

Richard Gregory, one of SASCon’s founders, said: “There isn’t a single digital marketing agency that hasn’t made generated income by building WordPress websites, and we are honoured to be able to recognise him with this award.”

---

## Make extensions for XBMC with Python

![](img/dd9251551a61a36067892b1cc68615b0_55_0.png)

Current media selection
List of installed plug-ins
Configure launcher
Rating (only available for hosted plug-ins)
Localised description string
Opens changelog for the plug-in

Python is the world’s most popular easy-to-use open source language. Learn how to use it to build your own features for XBMC, the world’s favourite FOSS media centre

### Advisor

Kunal Deo is a veteran open source developer. Currently he is leading two open source projects: WinOpen64 and KUNWiki. He is also a KDE developer. He has contributed to many open source projects, including KDE, Solaris, Beleenix and Openmoko

### Resources

- **XBMC:** www.xbmc.org/download
- **Python 2.7x**
- **Python IDE (optional)**

XBMC is perhaps the most important thing that has ever happened in the open source media centre space. It started its life on the original Xbox videogame console and since then it has become the de facto software for multimedia aficionados. It also has been forked into many other successful media centre applications such as Boxee and Plex. XBMC has ultimately grown into a very powerful open source application with a solid community behind it. It supports almost all major platforms, including different hardware architectures. It is available for Linux, Windows, Mac OS X, Android, iOS and Raspberry Pi.

In these pages we will learn to build extensions for XBMC. Extensions are a way of adding features to XBMC without having to learn the core of XBMC or alter that core in any way. One additional advantage is that XBMC uses Python as its scripting language, and this can be also used to build the extensions. This really helps new developers get involved in the project since Python is easy to learn compared to languages like C/C++ (from which the core of XBMC is made).

XBMC supports various types of extensions (or Add-ons): Plugins, Programs and Skins. Plugins add features to XBMC. Depending on the type of feature, a plug-in will appear in the relevant media section of XBMC. For example, a YouTube plug-in would appear in the Videos section. Scripts/Programs are like mini-applications for XBMC. They appear in the Programs section. Skins are important since XBMC is a completely customisable application – you can change the look and feel of just about every facet of the package.

Depending upon which category your extension fits, you will have to create the extension directory accordingly. For example...

```text
**Plug-ins:** plugin.audio.ludadi: An audio plug-in
plugin.video.ludadi: A video plug-in
script.xxx.xxx: A program
```

In this tutorial we will build an XBMC plug-in called LUD Entertainer. This plug-in will provide a nice way to watch videos from Reddit from within XBMC. Our plug-in will show various content such as trailers and documentaries from Reddit. We’ll also allow our users to add their own Subreddit. Each video can then be categorised as Hot, New, Top, Controversial etc. With this plug-in we will demonstrate how easy it is to hook into XBMC’s built-in method to achieve a very high-quality user experience.

Due to space limitations, we aren’t able to print the full code here. We are highly recommended to explore the cover disc to access the complete code, which has many other amazing functions.

---

### Make extensions for XBMC with Python

Use Python to create a new plug-in for XBMC

![](img/dd9251551a61a36067892b1cc68615b0_56_0.png)

#### 01 Preparing the directory structure

As we have mentioned previously, each XBMC extension type follows a certain directory naming convention. In this case we are building a *video* plug-in, so the plug-in directory name would be **plugin.video.ludlent**. But that's just the root directory name – we will need several other folders and files as well.

The following describes the directory structure of LUD Linux Entertainer:

```text
plugin.video.ludlent– Root Plugin directory
|-- addon.xml
|-- changelog.txt
|-- default.py
|-- icon.png
|-- LICENSE.txt
|-- README
|-- resources
|--- lib
|--- settings.xml
```

#### 02 Creating addon.xml

An **addon.xml** file needs to be created in the root of the extension directory. The **addon.xml** file contains the primary metadata from a XBMC extension. It contains overview, credits, version information and dependencies information about the extension.

The root element of **addon.xml** is the `<addon>` element. It is defined as:

```xml
<addon id="plugin.video.ludlent" name="LUD HSM Viewer"
version="0.0.1" provider_name="LUUK">
rest of the content is placed here
</addon>
```

Here, **id** is the identifier for the plug-in, so it should be unique among all the XBMC extensions, and **id** is also used for the directory name; **version** tells XBMC the extension version number, which helps in its ability to deliver automatic updates – XBMC follows the Major.Minor.Patch versioning convention; **name** is the English title of the plug-in.

**Note:** Steps 3 to 5 cover entries that need to be added within the **addon.xml** file.

#### 03 Adding dependency information

Dependency inside an extension is managed using the `<requires>` element.

```xml
<import addon="xbmc.python" version="2.1.0"/>
<import addon="plugin.video.youtube" version="3.0.0"/>
<import addon="plugin.video.vimeo" version="2.3.0"/>
<import addon="plugin.video.dailymotion_com" version="1.0.0"/>
</requires>
```

In the above code we have added a dependency to a library called **xbmc.python** version 2.1. Currently it is added as a mandatory dependency. To make the dependency optional you will need to add **optional="true"**; eg `<import addon="kumal.special" version="0.1.0" optional="true"/>`

In the above example we have added core dependency **xbmc.python** to 2.1.0 because it's the version shipped with XBMC version Frondo 12.0 and 12.1. If you were to add **xbmc.python** to 2.0 then it would only work in XBMC Eden 11.0 and not in the latest version.

For the current version of XBMC 12.1, the following versions of core XBMC components are shipped:

```text
xbmc.python 2.1.0
xbmc.gui 4.0.0
xbmc.json 6.0.0
xbmc.metadata 2.1.0
xbmc.addon 12.0.0
```

In addition to **xbmc.python** we are also adding some third-party plug-ins as dependencies, such as **plugin.video.youtube**. These plug-ins will be installed automatically when we install **plugin.video.ludlent**.

#### 04 Setting up the provider and entry point

Our extension is supposed to provide the video content for XBMC. In order to convey that, we have to set up the following element:

```xml
<extension point="xbmc.plugin.source" library="default.py">
<provides>video</provides>
</extension>
```

Here, the **library** attribute sets up the plug-in entry point. In this example **default.py** will be executed when the user activates the plug-in. The `<provides>` element sets up the media type it provides. This also gets reflected in the placement of the plug-in. Since ours is a video plug-in, it will show up in the Videos section of XBMC.

#### 05 Setting up plug-in metadata

Metadata about the plug-in is provided in `<extension point="xbmc.addon.metadata">`. The following are the important elements...

- **<platforms>:** Most of the time, XBMC extensions are cross-platform compatible. However, if you depend on the native platform library that is only available on certain platforms then you will need to set the supported platforms here. Accepted values for the platform are: all, linux, osx, osx32, osx64, ios (Apple iOS), win32 (Windows DirectX), win64 (Windows OpenGL) and android.
- **<summary lang="en">:** This gives a brief description of the plug-in. Our example set the language attribute as English, but you can use other languages too.
- **<description>:** A detailed description of the plug-in.
- **<website>:** Webpage where the plug-in is hosted.
- **<source>:** Source code repository URL. If you are hosting your plug-in on GitHub, you can mention the repository URL here.
- **<forum>:** Discussion forum URL for your plug-in.
- **<email>:** Author email. You can directly type email or use a bot-friendly email address like **max** at domain dot com.

#### 06 Setting changelog, icon, fanart and licence

We need a few additional files in the plug-in directory...

- **changelog.txt:** You should list the changes made to your plug-in between releases. The changelog is visible from the XBMC UI.

  An example changelog:
  - Initial Release
  - Fixed Video Buffering Issue

- **icon.png:** This will represent the plug-in in the XBMC UI. It needs to be a non-transparent **PNG** file of size 256x256.
- **fanart.jpg** (optional): The **fanart.jpg** is rendered in the background if a user selects the plug-in in XBMC. The art needs to be rendered in HDTV formats, so its size can range from 1280x720 (720p) up to the maximum 1920x1080 (1080p).
