# 3D Games

Most of the games I’ve mentioned so far are a little, well . . . two-dimensional. Sure, 2D games can be fun—I’ve certainly lost a significant portion of my life to Sudoku—but they don’t have the excitement factor that you get from shooting hordes of aliens or crashing a high-powered sports car into a wall.

Unfortunately, games designers have traditionally neglected Linux to concentrate on the significantly larger Windows market, so up until a couple of years ago there were few Linux-friendly 3D games to choose from. As the penguin has grown in popularity, however, people have started to take notice, and more Windows games now come with a Linux version.

The open source gaming community has come on leaps and bounds too, and there are some really high-quality games now. In this section I’ll run through a few of my favorites, after first making sure that your computer can handle the strain of 3D graphics.

# Checking for Hardware Acceleration

To play 3D games, you need a graphics card that can handle hardware acceleration. Without hardware acceleration, your computer’s processor has to try to do all of the fancy graphics rendering itself (a task for which it just isn’t designed), so your games end up running at a snail’s pace, if at all. Most modern graphics cards have some hardware acceleration support built in, but whether it is enabled will depend on the state of the Linux driver for your card. You can find out how good 3D support is for your graphics card at https://wiki.ubuntu.com/HardwareSupportComponentsVideoCards/.

If you just want to know whether you have the minimum level of acceleration required to play games, then open a Terminal (Applications ▸ Accessories ▸ Terminal), type glxinfo | grep rendering, and press ENTER. (That vertical line is the "pipe" symbol and can normally be inserted by pressing SHIFT and \ on your keyboard.) If you get a message telling you that glxinfo isn’t installed, use the Ubuntu Software Center to install mesa-utils and then try again.

If hardware acceleration is enabled, you’ll see direct rendering: Yes appear in the Terminal. That’s good news, because it means you can skip to the next section and sink your teeth into some three-dimensional gaming goodness.

If you received the message direct rendering: No instead, you’ll need to install different graphics drivers if you want hardware acceleration to work. See "Games/Compiz Don’t Work: Installing Accelerated Graphics Drivers" on page 394 for instructions.

> NOTE Many of the default graphics drivers for Linux can’t handle anti-aliasing, which is the feature that removes jagged edges from graphics, making them look smoother and more life-like. If you can’t live without anti-aliasing, you should also see Chapter 21 for information on installing a better graphics driver.