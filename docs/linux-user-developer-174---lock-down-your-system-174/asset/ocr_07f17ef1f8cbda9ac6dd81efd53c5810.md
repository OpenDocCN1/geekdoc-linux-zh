# A Raspberry Pi photo frame

With some Python code and a nice display screen, you can turn your Raspberry Pi into a very nice photo frame

![](bbox=[0.05, 0.26, 0.18, 0.36])

Joey Bernard is a true Renaissance man, splitting his time between building furniture, helping researchers with scientific computing problems and writing Android apps

In a previous article, we looked at using Kivy as a cross-platform graphical interface framework that you can use with your Raspberry Pi. Unfortunately, we did not have the room to really look at any possible uses. This issue, we will look at one possible use, that of displaying photos on some kind of display. This might be something you do at home, with family pictures, or it could be a slideshow for a business or event. If you didn't get a chance to read the previous article, that is okay. We will review enough of the basics that you should be able to get off to a running start now. You will obviously need a physical display attached to your Raspberry Pi to show the images on. There are several options available, such as the official 7-inch touch screen. You can also use anything that accepts HDMI as input. You will also need your Raspberry Pi to start up the X11 server when it boots up. By default, Raspberry should do this. But, if you have disabled the X11 server and only use the console, you will need to either re-enable the desktop or just reinstall the OS to have a clean start.

The first step is to be sure that the Kivy packages are installed on your Raspberry Pi. If you are running Raspbian, you can do this with the command

```
sudo apt-get install python-kivy python-kivy-examples
```

This also installs a collection of good examples that you can use as jumping-off points for further projects. With Kivy, you subclass the App class to create the graphical interface. The core of the Python script would contain the following code

```
sudo pip install kivy
```

The commented section of this core code is where we will need to pull out all of the Python code that does the work of loading images and displaying them. The first step is to get the list of image files to use as part of the photo frame. There are several different ways you could do this. If you wanted to simply use all of the images within a subdirectory, you could create the list with the code here:

```
# get all images in a subdirectory

current_dir = dirname(__file__)
filelist = glob(join(current_dir, 'images', '*'))
```

This pulls all of the files in the subdirectory named 'images'. If your images are scattered around your filesystem, it might be better to use a text file containing the locations for each of the files you want to use. In this case, you would want to accept the following code

```
in_file = open('filelist.txt')
temp = in_file.readlines()
in_file.close()
filelist = []
for line in temp: 
    filelist.append(line.strip())
```

We need to use the strip method because the readlines method of the file object includes the newline character at the end of each line. We need to remove these before we can use them later on when we go to load the images. The next step is to actually display the images. The simplest method is to just pop them up on the screen, one at a time. But this is a bit boring. Instead, we could use the available Carousel object to handle transitioning the image from one to another. The following code shows how to create this type of display.

```
import kivy
from kivy.app import App
from kivy.uix.image import Image

from kivy.uix.carousel import Carousel
from kivy.clock import Clock

class PhotoFrameApp(App): 
    carousel = Carousel(direction='right', loop=True)
    def my_callback(self,dt):
        self.carousel.load_next()
    def build(self):
        # Use the filelist generation method of choice
        for curr_image in filelist: 
            image = Image(source=curr_image)
            self.carousel.add_widget(image)
        Clock.schedule_interval(self.my_callback, 2.5)
        return self.carousel
if __name__ == "__main__": 
    PhotoFrameApp().run()
```

# Why Python?

It's the official language of the Raspberry Pi. Read the docs at python.org/doc

> "You subclass the App class to create the graphical interface"

In the previous code, the carousel object was set to loop. This means that when you reach the end of the list of images, it will simply loop back around to the beginning of the list, continuing forever. The next portion defines the callback for the updating of the carousel. It simply calls the 'load_next()' method of the carousel to pull up the next image on the list. In the 'build()' method, the first step is to create the list of image filenames. You could use either of the methods suggested earlier, or one of your own devising. Once you have that list, you can loop through each of them and create a new Image object for each of them. These new Image objects are added to the carousel with the 'add_widget()' method. The last step in the 'build()' method is to create a schedule using the Clock object. Using the 'schedule_interval()' method, this code will change the image every 2.5 seconds. This method is good as a first start, but what if you want a more interesting transition between images? This can be done by using another set of classes called Screen and ScreenManager. If your list of images don't take up too much RAM, you can simply create a new Screen object