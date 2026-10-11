# **How I made: Pikon**

![](bbox=[0.07, 0.12, 0.22, 0.27])

# # How I made:
# PiKon

**3D-printed telescope meets RasPi camera**

**Tell us how you began your project**
**Mark Wregley** I run this small company called Alternative Photonics and like to find out about new technologies. When Sheffield's Festival of the Mind came along I thought of what could we put together in terms of things that are new and disruptive, and that's how the whole project started. The two things I was interested in were using Raspberry Pis for photography and 3D printing. With 3D printers you've got a device in the ballpark of £500, putting it amongst the price you'd pay for consumer items, so manufacturing is something you can do at home. There are companies who will print something for you, so you send in a design and they'll produce it. And there are maker communities - Andy runs a group called Sheffield Hardware Hackers and Makers.

**Andy Kirby** Sheffield Hardware Hackers and Makers is for anyone off the street to come along to if they want to hack and make things. I set it up as part of the original RepRap project that ran on the Internet quite some years ago (Ed: RepRaps are 3D printer kits that can print parts for more RepRaps). I found that there were quite a few people building printers who got to a certain point and then got stuck, so I set up this group originally to be a drop-in for people to come along to and get the help they needed.

**Andy, what was your role in the PiKon?**
**Andy** I helped Mark pick a 3D printer that was going to be pitched right for his skillset and then, as he was building up the printer, when he got to bits where he got stuck he'd bring it along to the Hardware Hackers group and say "I'd shouldn't do this right" or "I can't get it to do that," and we'd work through the problems together. Once he'd got his printer going, I worked through the CAD software with him to see what was available that was open source and within his capabilities. There are various things you can't do with a 3D printer when you design parts, so we had a conversation about that and I gave him the shortcut to get working parts out quicker.

**How does the PiKon work?**
**Mark** Most telescopes work on the principle that you have some sort of object lens or mirror which forms an image and then you use an eyepiece to examine that image, so it's usually what's termed as a virtual image. With the PiKon, what we're doing is using the objective device, in this case a 4.5-inch (355mm) mirror, to form an image and then placing the Raspberry Pi camera without its lens - so just as a sensor - where the image is formed. So effectively, instead of using an eyepiece we're examining the image electronically by placing the Raspberry Pi sensor there, and the sensor is substantially smaller so we're able to examine a fairly small area of the image.

**What kind of resolution do you get?**
**Mark** At the moment, the setup that we've got is equivalent to a magnification of about 160. If you look at the Moon, the field of view of your eye is about half a one degree, the PiKon's maximum field of view is about a quarter of one degree, so effectively you can see about half the moon in full frame. The next thing I'd like to do is look at planets. In terms of its resolution, the PiKon's sensor is five megapixels, which is 2500x2000 pixels. If you're going to reproduce an image in print you'd normally use something like 300dpi, so 5MP would allow you to reproduce something like an A4 image. On a computer screen all you need is 72dpi, so what I'm quite interested in doing next is seeing how much magnification we can get simply by cropping - so literally throwing away some of the pixels to be able to zoom in on something like a planet. If you read the Astronomy for Beginners stuff, they talk about needing a magnification of 200-250 to be able to observe planets, so I'm hoping we can do things like see the rings of Saturn. We're not out to rival the Hubble - we think that what you've got in a reasonable instrument and you can do a few interesting things with it. The other thing is that because it's using a Raspberry Pi sensor instead of an eyepiece, you're immediately into the world of astrophotography rather than doing observations, so that's the sort of way we're going.

**How do you control the PiKon's camera?**
**Mark** We would like to do it better!
**Andy** At the moment it's done through the command line. I'm not a Raspberry Pi programmer... So we're using Raspberry Pi at the moment, which gives you a certain number of seconds of preview and then takes the picture, so it's a bit clunky. I'm talking to a guy who's into Raspberry Pi and is also a photographer, and he's written some programs where you have a shutter button. The next thing to do then is to control PiKon from an input/output device like a shutter button and then give the JPG files you produce a sequential or a date-stamped filename. One thing I'd like to see next is if we could get this hardware out into the public and attract people to actually come along and develop more and more software for it. I tried taking pictures of the International Space Station with an ordinary camera, for example. It's really difficult because suddenly this dot comes flying across the horizon and you have to swing around, get your camera lined up, press the shutter and so on. One thought I had was it would be nice if you could take multiple shots with the PiKon - you press a button and it keeps taking a photograph every five seconds.

![](bbox=[0.76, 0.27, 0.86, 0.39])

**Mark Wregley**
is a member of the Institute of Physics and holds a Licensitship with the Royal Photographic Society

![](bbox=[0.76, 0.49, 0.86, 0.61])

**Andy Kirby**
is an early contributor to the RepRap project and runs the Sheffield Hardware Hackers and Makers group

**Like it?**
The Raspberry Pi Foundation website featured a project that mounts the Pi and camera onto a telescope and captures great images bit.ly/1qYTp3Bp

**Further reading**
If you're interested in astrophotography and developing software for PiKon, check out these astronomy packages: bit.ly/10Wj6E5

# The setup we've got is equivalent to a magnification of about 160