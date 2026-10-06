# 3D Games

Most of the games I've mentioned so far are a little, well . . two-dimensional. Sure, 2D games can be fun—I certainly lost a significant portion of my life to Sud—but they don't have the excitement factor that you get from shooting hordes of aliens or crashing a high-powered sports car into a wall. Unfortunately, game designers have traditionally neglected Linux to concentrate on the Windows market, so up until a couple of years ago, there were few Linux-friendly 3D games to choose from. As the penguin has grown in popularity, however, people have started to notice, and more Windows games now come with a Linux version.

The open source gaming community has grown by leaps and bounds, and there are really high-quality games now. In this section, I'll run through a few of my favorites, after first making sure that your computer can handle the strain of 3D games.

# Checking for Hardware Acceleration

To play 3D games, you need a graphics card that can handle hardware acceleration. Without hardware acceleration, your computer's processor has to try to do all of the fancy rendering itself (a task for which it isn't designed), so your games end up running at a snail's pace, if at all. Most modern cards have hardware acceleration support built in, but whether it will depend on the state of the Linux driver for your card. You can find out how good 3D support is for your graphics card at https://wiki.ubuntu.com/HardwareSupportComponentsVideo/

If you want to know whether you have the minimum level of acceleration required to play games, then bring up the Desktop, open a Terminal, type glinfo | grep rendering, and press ENTER. (That vertical line is the "pipe" symbol and can be inserted by pressing SHIFT and \ on your keyboard.) If you get a message telling that glinfo isn't installed, use the Ubuntu Software Center to install mesa-utils and then try again.

If hardware acceleration is enabled, you will see direct rendering: Yes appears in the Terminal. That's good news, it means you can skip to the section and skip your teeth into some 3D gaming goodness.

If you received the message direct rendering: No instead, you'll need to install different graphics drivers for hardware acceleration to work. See "Games/Unity Don't Work: Installing Accelerated Graphics Drivers" on page 392 for instructions.

> Many of the default graphics drivers for Linux cannot handle anti-aliasing, a feature that removes jagged edges from graphics, making them look smoother and more lifelike. If you can't live without anti-aliasing, see Chapter 22 for information on installing a better graphics driver.