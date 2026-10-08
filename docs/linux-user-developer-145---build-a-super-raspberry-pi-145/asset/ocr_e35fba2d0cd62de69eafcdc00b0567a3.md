# Python column

![](bbox=[0.07, 0.15, 0.16, 0.24])

**Joey Bernard**
As a true renaissance man, he splits his time between building furniture, helping researchers with scientific computing problems and writing Android apps

# Turn your Pi into a motion sensor with SimpleCV

Learn how to implement facial recognition into your Raspberry Pi using Python and a webcam

# Why Python?

It's the official language of the Raspberry Pi. Read the docs at [python.org/doc](python.org/doc)

Back in *issue 142, we looked at* using the Kinect with the Raspberry Pi. But not everyone has access to this kind of hardware. Another class of project that is popular with Raspberry Pis is using USB cameras to create monitors of one form or another. A lot of these projects use command line applications to talk to the USB camera and generate images or movies that are used as part of the system. But what if you are writing your own program in Python and you want to add some form of image system to your code? Luckily, there are several modules available for you to choose from. In this article, we'll take a look at using SimpleCV to get your program to talk with the USB camera. SimpleCV is built on top of OpenCV, making it easier to use for common tasks. Assuming you are using Raspbian, you can go to the main page for SimpleCV ([www.simplecv.org](www.simplecv.org)) and download a DEB file. To install it, you can simply run:

```
```bash
sudo dpkg -i SimpleCV-1.31.deb
```
```

Before you do, however, you will want to install all of the dependencies. You can do that with the command:

```
```bash
sudo apt-get install python-python-support python-numpy python-scipy python-python-opencv python-pyaudio python-setuptools
```
```

You can check that everything worked by running the command `simplecv` at the command line. This will start Python up and run the interactive shell that is provided by the SimpleCV module. You can then try connecting to your USB camera and pulling images from it.

Now that everything should be up and running, how do you actually use it in your own code? You can load all of the available functions and objects into the global scope with the command:

```
```python
from SimpleCV import *
```
```

Making sure that you have your USB camera plugged in, you can now create a camera object with:

```
```python
cam = Camera()
```
```

This will load the required drivers, and initialise the camera so that it is ready to start taking pictures. Once this object creation returns, you can grab an image from the camera with:

```
```python
img = cam.getImage()
```
```

At least in the beginning, when you are experimenting, you may want to see what this image looks like. You can do this with:

```
```python
img.show()
```
```

You will, of course, need to have a GUI up and running in order to actually see the movie. Otherwise, you will get an error when you try and call `img.show()`. Don't forget that you can always pull up documentation with commands like:

```
```python
help(cam)
help(img)
```
```

With the `Image` object, you can do some basic processing tasks right away. You can scale an image by, say 90%, with `img.scale(0.90)`. You can also crop an image by giving it a start location and saying how many pixels across and how many up and down you want to crop. This looks like `img.crop(100,100,50,50)`. SimpleCV has the location (0,0) as the top-left corner of an image.

The really interesting functionality in SimpleCV is the ability to find features within an image and to work with them. One of the clearest features that you can look for is blobs, where blobs are defined as continuous light regions. The function `img.findBlobs()` will search the captured image for all blobs and return them as a FeatureSet. You can set the minimum number of pixels to consider a single blob, the maximum number of pixels, as well as a threshold value. If you are looking at a region that has some hard edges, you can use the function `img.findCorners()`. This function will return a FeatureSet of all the corners within the captured image. A very simple monitor program could use one of these functions to see if there is any motion happening. If there is, then the set of blobs or corners will change from one frame to another. Of course, a little more reading will lead you to the `img.findMotion()` function. This function will take two subsequent images and see if any motion can be detected going from one to the other. The default method is to use a block matching algorithm, but you can also use either the Lucas-Kanade method or the Horn-Schunckl method.

The above methods will let you know some features of the captured images, and if any kind of motion has occurred. But what if you are more interested in identifying whether people have been moving around? Maybe you have an area you need to secure from espionage.

> SimpleCV is built on top of OpenCV, making it easier to use for common tasks