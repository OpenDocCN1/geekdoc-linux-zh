
## Roundup
GIMP >> RawTherapee >> Darktable >> LightZone >> Pixelluvo

![](img/3f314b57ad3c8b08d25e5d1ab47de56d_159_0.png)

Alexander Tolstoy likes nothing better than rolling up his metaphorical sleeves and seeing what new gems the open source community has to offer.

## Photo editors

Keen photographer Alexander Tolstoy keeps his imperfect snaps, for fixing later, using some of the best photo editors available for Linux.

### HOW WE TESTED...

Editing photos isn't the same as editing general images. Therefore we decided to compare some of the best photo editors for Linux with a focus on fixing common faults, enhancing colours and lost details that might be considered gone for good. The aim here is to help you select the most feature-packed and practical software that can bring dull images back to life. We'll take a closer look at their advanced features, such as automatic enhancements, the ability to fix dull, blurry, under- or over-exposed images and, of course, whether or not they handle RAW files.

It's not the first time we've run a Roundup on image or photo editors, but this current group includes a different selection of software. Four out of the five are open source tools (although **Lightzone** had been a proprietary application in the past). The fifth is a commercial option, which is perhaps less known to the reader, but should be of great interest to photo-editing enthusiasts. Read on to find out more!

![](img/3f314b57ad3c8b08d25e5d1ab47de56d_159_1.png)

When it comes to selecting a photo editor, there's plenty of choice. There are general-purpose editors like GIMP or Pinta, image library managers with editing features, such as Digikam or Shotwell, and finally there's software for digital artists (think Krita). Our interest lies in fixing photos and processing RAW files, so we grabbed GIMP with its set of built-in effects, Ufrav plugin, and lots of third-party plugins from FX Foundry and G'MIC. Then we included Darktable and RawTherapee – two classic darkroom editors with tools for dragging out barely visible details. Lightzone is similar to these two programs, but has a more consumer-friendly interface. Last but not least is Pixelluvo, a paid-for program with a limited set of editing features. GIMP is the only contender that doesn't use a dark UI theme by default. Although a dark theme adds a 'pro' feel to the program, it won't hide the truth in our Roundup!

### Availability

How to get a program working...

Sometimes it requires extra efforts to obtain and install a program. You might have to visit its web site and find the correct download option. There are no such issues with GIMP because it’s included with every Linux distribution, but we’re working with a supercharged GIMP installation, packed with extra plugins. GREYC’s Magic for Image Computing might be available in your system’s package repositories, but if not you can grab it from https://gmic.eu, unpack the archive and put the executable file in `~/.config/GIMP/2.10/plug-ins`. The FX Foundry pack has its own page at www.gimpfx-foundry.sourceforge.net and similarly it should be unpacked into a neighbouring directory in `~/.config/GIMP/2.10/scripts`. Although there’s nothing difficult about this requirement, novice users may consider such extra actions to be an advanced task.

**RawTherapee** and **Darktable** already come with everything bundled inside the software packages. Those two programs are rarely included in distributions’ default offerings out of the box, but they’re always available in online repositories – just check it with your software store or package manager. However, **Darktable** scores more in this test because it’s also available in Snapstore and Flathub, while **RawTherapee** has only an AppImage.

The way **Lightzone** is distributed is somewhat cumbersome. Due to the proprietary legacy, the official project web site still lists outdated information, which might confuse some users who want to get the application. However, **Lightzone** is based on Java, which means it should be a platform-agnostic application, and so it’s often packaged for many Linux distros. Ready-to-use packages exist for Ubuntu, Fedora and openSUSE and many others. For Ubuntu-compatible distros you can use the PPA at **ppa:lightzone-team/lightzone**.

**Pixelluvo** costs money, $34 to be precise. The official web page offers 30-day trial downloads, with DEB and RPM packages for Ubuntu and Fedora, respectively. Those packages can be used for other RPM- and DEB-based distributions as well, or repacked for other flavours of Linux (treat **Pixelluvo** downloads like archives). **Pixelluvo** includes a static set of the old Qt4 libraries at `/opt/pixelluvo/libs64`, which you may want to delete in order to force the program to use your system’s libraries. We’ll admit that this is a non-trivial task for many users. Additionally, the trial version doesn’t enable saving modified images with sizes larger than 800×600. We recommend making those tweaks!

![](img/3f314b57ad3c8b08d25e5d1ab47de56d_160_0.png)

| VERDICT | GIMP | DARKTABLE | RAWTHERAPEE | LIGHTZONE | PIXELLUVO |
| :--- | :---: | :---: | :---: | :---: | :---: |
| **Score** | 9/10 | 10/10 | 9/10 | 8/10 | 7/10 |

There are many easy methods of getting hold of and installing Darktable.

### Ease of use

How user-friendly is each of our five contenders?

Previously, GIMP was a mess of floating windows that required a lot of manual arrangement. Nowadays the program uses the single-window mode by default. Its photo-editing features are located in different places under Filters > Enhancing menu, Filters > G'MIC-Qt and a separate top-level menu for FX Foundry. Unless you know where your tools are beforehand, it isn’t easy to find them.

**Darktable** has no such fragmentation. However, you first need to point the application to the directory with your images and then select one for editing. By default, the editing tools are hidden under the categories on the right side of the screen. **RawTherapee** has a more thoughtful UI design. It’s similar to the one in Darktable, but you don’t lose the file manager tree on the left when editing an image. Furthermore, all the useful tools are already expanded in the right panel. Similar to Darktable, Lightzone suggests switching between browsing and editing modes. When editing, each filter or tool is presented like a separate floating panel, which you can turn off or on.

Our remaining program, Pixelluvo, also shone in terms of usability. Photo-editing capabilities could be found under the Colour and Effect sections of the top menu bar. Pixelluvo was designed with simplicity in mind, and consequently it was nearly impossible to get lost in its clear and simple lists of available tools.

![](img/3f314b57ad3c8b08d25e5d1ab47de56d_160_1.png)

| VERDICT | GIMP | DARKTABLE | RAWTHERAPEE | LIGHTZONE | PIXELLUVO |
| :--- | :---: | :---: | :---: | :---: | :---: |
| **Score** | 7/10 | 8/10 | 10/10 | 10/10 | 10/10 |

Having frequently used tools at hand is the key to winning our usability test.

### Fixing colours, shadows and more

Want to give your photos a natural look?

We may prefer one tool over another purely for subjective reasons, but there are some practical tests that expose the real value of each photo-editing program.

For this Roundup we used a couple of images as test subjects when exploring the five programs. One was a scanned historic colour film frame with inadequate lighting, film grain and insufficient exposure; while another was an unprocessed RAW shot of a night urban scenery with illumination, which was also underexposed.

The aim was to try to achieve the best possible results from both shots in each of our five programs. We paid special attention to the white-balance fixer and any available colour adjustment sliders, as well as the shadows, highlights and level correction tools.

In the end, a good program is one that can either fix everything using automatic algorithms, or by offering adequate tools for manual work. It goes without saying that the only acceptable editing mode is a non-destructive one, where the user can always roll back to the original image without losing anything irreversibly.

![](img/3f314b57ad3c8b08d25e5d1ab47de56d_161_0.png)

**Gimp**

When it comes to correcting colours, Gimp shines thanks to its fast GEGL engine. We didn’t need any third-party plug-ins for fixing the colours of our test photo. The Colour>Levels menu enabled us to fix the white balance (look for three pickers for choosing black, grey and white spots), but we also managed to remove that distasteful green hue on certain parts of the image by adjusting levels manually for green channel only. Using Gimp’s standard features for tuning up levels and curves turned out to be easier than in specialised software such as RawTherapee and Digikam. Not that one application is better than another, but Gimp is just easier to use for an average user.

When processing RAW files, Gimp can integrate with UFRaw, RawTherapee and possibly other similar tools. The result depends on how well a user can handle the many tools of a RAW processor.

*Score: 10/10*

**Darktable**

Darktable has some advanced tools for working with colours, including a dedicated White Balance section. The neutral Color Picker tool sits under the Levels section, but it’s not intuitive and takes quite a lot of time to fix white balance. Getting this tool to work correctly in Darktable is crucial. We achieved acceptable results by adjusting the colour temperature and each of RGB channels separately. We believe that Darktable has too many tools, many of which overlap, so the program is more likely to help you achieve artistic effects than bring back natural colours.

The positive side of Darktable was working with RAW files. For example, the application offers the original algorithm for exposure compensation, which resulted in a pleasing image with less noise and better local contrast. Another Darktable-only tool is Velvia, which boosts image saturation for brighter parts of the image only.

*Score: 6/10*

### Removing image noise

How good are these programs for eliminating noise and restoring detail?

The reason why we equipped Gimp with third-party plug-ins is because they grant the program advanced tools for combating colour noise and removing grain. The Repair category inside the G'MIC interface contains some advanced denoising filters, of which the most powerful is perhaps Iain’s Noise Reduction. This filter contains a range of configurable options that effectively remove film grain or colour noise that has been created by high ISO values.

We managed to achieve reasonable results simply by combining several filters in succession. However, the built-in options for reducing noise and grain in Darktable proved to be even more efficient because they managed to preserve details more effectively. Darktable has a bilateral denoise feature for high ISO; the non-local tool can be used when denoising chrome and luma; there’s a dedicated chromatic denoise tool for RAW images; and the universal Equalizer tool can enhance many things, including clarity as well and reduce colour noise. RawTherapee’s denoising tools are slightly less effective, but when it comes to processing RAWs with high ISO, we think RawTherapee has the edge because it produces much smoother JPEGs compared to those processed by Darktable.

In contrast to the other programs, Lightzone just has a simple denoise tool with only two sliders for colour and grain. Sadly, for some of our test images, that denoise filter had little or no effect.

Finally, the Reduce Noise feature in Pixelluvo is only there for the sake of box-checking. It works as a primitive median filter and removes noise together with precious details. It’s best avoided unless you want to change the nature of your original photo.

| VERDICT | GIMP | LIGHTZONE | DARKTABLE | PIXELUVO | RAWTHERAPEE |
| :--- | :---: | :---: | :---: | :---: | :---: |
| **Score** | 8/10 | 5/10 | 8/10 | 5/10 | 10/10 |

Choose Gimp for retouching old photos and go with RawTherapee for creating perfect JPEGs out of your RAW shots.
