
## REAL SOLUTIONS for REAL NETWORKS

ADMIN is your source for technical solutions to real-world problems.

Improve your admin skills with practical articles on:

- Security
- Cloud computing
- DevOps
- HPC
- Storage and more!

![](img/b40e8bf6cf651f8eebf36f5265123095_64_0.png)

## GET IT FAST with a digital subscription!

## 6 issues per year!

**ORDER NOW**

shop.linuxnewmedia.com

![](img/b40e8bf6cf651f8eebf36f5265123095_65_0.png)

# MakerSpace

Get creative with the FLUX Beamo laser and open source software

## Beam Me Up, Fluxy!

![](img/b40e8bf6cf651f8eebf36f5265123095_65_1.png)

> With the FLUX Beamo laser and a Raspberry Pi Board B10001, you can execute your own laser cutting projects on a wide range of materials. *By Christa and Ian Travis*

Laser cutting mainly used to be the purview of hard-headed business owners with solid financial backing and a business plan to make sure the laser paid for its upkeep. And there were hobbyists who were more interested in the arts and crafts side of laser cutting and saw the laser as a tool for cutting and engraving materials such as wood, cloth, and acrylics in the scope of their arts and crafts projects. The trouble was, many people were more than a little worried about the Heath Robinson-style, low-budget lasers they could purchase at the time. The foundations of the laser world were to be shaken though, when FLUX – an organization founded by a "group of passionate young engineers and designers," as the manufacturer itself states – launched the Beebox laser cutting machine back in 2018. FLUX quickly followed up with the Beamo, promoted as "the world's smallest laser cutting machine" the next year.

The FLUX laser family not only meant a paradigm shift in terms of laser cutting machine pricing, but also a move towards a community-driven approach. For one thing, the FLUX laser family relies on a Raspberry Pi, in the form of the Raspberry Pi Board B10001 [1], to control the machine. And the downloadable software package that lets users send their ideas (in the form of, say, PNG images or vector diagrams) to the laser runs on your choice of operating system, whether this be Windows, macOS, or Linux. Expanding on the community idea, FLUX users can get together to exchange ideas on Facebook or at regular FLUX community meetings that take place all over the world – even in Germany, where we're based. So, laser-afine readers, let's get started with unboxing and the setup on the hardware and software side.

### Unboxing

The FLUX Beamo reaches its new owner in a very large and fairly heavy cardboard box. If you are worried about the state of your back, then it's a good idea to ask a friend to help you lift the beast out of the box. Once you've done this, there are a couple of tasks to complete before you get started on your first project. Besides doing the obvious things like removing the vent hose and attaching it to the duct on rear of the laser with the clamp kindly provided by the supplier, attaching the WiFi antenna, and plugging in, there is also the software setup. This no big deal: After powering on your laser cutter, select *Network on the Start screen* (Figure 1) and then *Connect to Wifi* if you are using the machine's wireless interface. Choose a WiFi network, enter the password, and let DHCP do its magic. You can alternatively use the Ethernet cable provided – this can be a good idea if the WiFi connection is too slow or unreliable. Once the machine has an IP address, make a note of the address and move on to the next stage, installing Beam Studio.

![](img/b40e8bf6cf651f8eebf36f5265123095_65_2.png)

![](img/b40e8bf6cf651f8eebf36f5265123095_66_0.png)

**Beam Studio**

If you worked with CO2 lasers prior to 2009, one of the biggest items on your wish list was probably a camera with software support that let you see what the laser was "seeing." Something that would take the guesswork out of positioning the laser head and alleviate any worries about lasering beyond the edge of the medium. Amazingly, considering its low price compared to the laser behemoths of the past, the FLUX laser family has exactly that in the form of a built-in camera and Beam Studio.

![](img/b40e8bf6cf651f8eebf36f5265123095_66_1.png)

![](img/b40e8bf6cf651f8eebf36f5265123095_66_2.png)

To install Beam Studio (Figure 2), go to the FLUX website [2] and select the version that matches your operating system. If you have a recent Ubuntu system, this will be v.1.8.3 -Ubuntu-18.04 x64. The name of the install file is beam-studio_1_8_3_amd64.deb, and you can install it using the Ubuntu package manager.

Right-click on the downloaded file, then select Open with other application, and then select Software Install. The installer prompts you for your password and then sets about installing Beam Studio. If you picked the DEB package up directly from FLUX, you can ignore the warnings about the software being potentially unsafe.

Beam Studio asks you to set up an account and then prompts you to choose how to connect to your laser cutter (Figure 3). You can also optionally choose to calibrate the camera (Figure 4).

**Test Job**

FLUX thoughtfully provides a tiny piece of plywood and a test job to help you get started. It’s a good way of finding out if your laser is correctly aligned. If it isn’t, see the “Smoke and Mirrors” box.

![](img/b40e8bf6cf651f8eebf36f5265123095_66_3.png)

the piece of plywood on the grid and follow the procedure to set the focus of your laser – either fold down the piece of Perspex for a manual focus, or use the optional autofocus feature. Now click on the camera icon and drag a frame around the area where you placed the piece of plywood. This tells the laser cutter to switch on the camera and scan for the exact position of the wood. Then select File | Example and load the imaginatively named Example of Beamo file. As you can see from Figure 2, the file consists of two layers, a bitmap image with the hello beamo logo, and a single ring to cut out the engraving. This is an important feature. Layers let you engrave a bitmap image onto a suitable material such as wood or acrylics in one layer, and the cutting work with a simple vector image is assigned to a different layer with different parameters.

Group the two images and center them on the plywood. The default parameter settings were chosen by FLUX and will be perfect for the job using the piece of plywood provided. Press Go, and then in the Beamo window that appears, press the arrow button to start the job. If all of this worked, you are well on your way to getting creative with your FLUX laser. The next part of the journey involves creating your own designs on paper and scanning the results for post-processing with a software tool capable of handling both vector and bitmap images. In the Linux world, and beyond, the tool of choice here is likely to be Inkscape.

### Smoke and Mirrors

As you are probably aware, laser cutters are precision instruments. What you may not have been aware of up to this point is that the laser beam is deflected by mirrors to the laser head. Any knocks the laser's packaging took en route to its new owner are likely to cause some misalignment issues. You may get lucky and not need to align the mirrors on your machine, and you may not. We were not so lucky and had to align the first reflecting mirror (Figure 5), which involves removing a large number of Allen screws before you can start the alignment. It sounds complicated, but if we managed it, we're sure you can, too. Here's what you need to do:

1. **Mirror one:** With the laser switched off, attach a piece of white sticky tape (that's why it's included in the scope of supply) to mirror number one. Close the laser's lid and switch the power on. On the touch panel, tap Maintain. On the maintenance screen, tap Motors. Then move the laser head manually to the top left position after doing so. Now press Laser Pulse to fire one shot at the tape (you should see a puff of smoke) and make sure you can see a dot. Now, move the laser head manually to the bottom left position. Make sure the lid is closed and fire another shot at the tape. If the dots from the laser head line up, you can move on to the next mirror. If they don't line up, adjust the screws on mirror number one and repeat the steps until the mirrors are lined up. If the second shot misses the tape entirely, move the head to center left position to check the direction in which you need to adjust. Turning the top left screw clockwise moves the dot down and to the left. Turning the top right screw clockwise moves the dot to the right, and moving the bottom screw moves the dot upward. Easy. All done. Now for mirror number two.
2. **Mirror two:** This time attach a piece of sticky tape to the metal ring on mirror three. Move the laser head to the center left position. Close the lid again and fire a shot. Then move the laser head to the center right position and fire another shot. The dots need to overlap. If not, adjust the screws on the second mirror until everything lines up. The screws are in different places and do different things this time. If you are really unlucky, you may need to adjust the laser head, the laser tube, and the third reflecting mirror, too. We're not going to go into the procedures for doing so here, but again, it's all smoke and mirrors. You may need to RTFM (which naturally means Read the FLUX Manual) at this point if you really need these adjustments. But let's hope you were lucky and can move straight to the first actual laser engraving and cutting task.

## Inkscape

Installing Inkscape on Ubuntu is as easy as pie. If this amazing, free program

![](img/b40e8bf6cf651f8eebf36f5265123095_67_0.png)

isn't already installed, simply launch the Ubuntu Software Center and type Inkscape in the search box. Then type your password when prompted, and wait for Inkscape to install. Now it's time to get creative: Christa had this idea for a Christmas decoration showing the Three Wise Men, a star, and a camel. With her being one of those fortunate people who can imagine a scene in their heads and draw it on paper without needing photos or sketches as a reference, she just sat

![](img/b40e8bf6cf651f8eebf36f5265123095_67_1.png)
