
## Webcams

### Webcamoid

We recently looked at the brilliant cameratris, a tool for editing your webcam settings while it is being used. Cameratris was particularly useful for video conferencing because it enabled you to adjust the brightness, exposure, and color balance while you were in a meeting. But cameratris could only adjust parameters supported by your hardware and couldn't process the images itself. This is trickier to achieve because it requires more than simply changing device settings and instead requires the video stream to be intercepted, processed, and passed on to a destination as quickly and efficiently as possible. The amazing OBS Studio can do this, and so too can Webcamoid.

Webcamoid is a far more modest desktop application than OBS Studio. Rather than being an entire suite of tools for live-streaming, it's a far more focused photo and video effects processing tool. This makes it less resource hungry and easier to use. It can record videos and take photos from your webcam, capture your desktop, and run captures through one or more of over 60 effects. Alongside the same inbuilt settings you can control with cameratris, you can turn your video into ASCII, a cartoon, or a black and white movie, with or without distortion, blurring, and aging. These and many other effects can be stacked and exported to any format supported by FFmpeg, which is driving the processing. Like OBS, Webcamoid can install its own virtual webcam driver so that processed video with its audio can be passed through to another application. After setting this virtual device as the source, any application accessing this virtual device will receive the processed video as if it were a live feed, which is a great way to improve the quality of your own video meetings, or at the very least, make them more interesting.

![](img/e3f454b04d121b3b3750fddfda8dd21e_84_0.png)

![](img/e3f454b04d121b3b3750fddfda8dd21e_84_1.png)

If you're unhappy with the built-in effects you find in Zoom or Google Meet, run your streaming video through Webcamoid first.

**Project Website**
https://webcamoid.github.io

## Text Editor

### Pulsar

There are many projects whose popularity only becomes clear when those projects came to an end. Canonical's Unity desktop is a good example of one that also continues to thrive as a community project, and so too is GitHub's now defunct text editor, Atom. Atom was a code and text editor that became the torch-bearer for a new generation of graphical editors whose functionality could be profoundly changed with plugins and a configuration file. More importantly, it was built using Electron - the web-based framework that enabled developers to build desktop applications with web technologies - and Electron was built for Atom. This synergy between the two lasted until the end of 2022 when GitHub ceased its active development of Atom, at which point its immense popularity became apparent. For any such popular open source applications, that really just signals the end of the beginning.

Pulsar is a community and open source continuation of the original Atom code editor and IDE. Like the original, and as you might expect from a modern web framework, it's fantastically well designed, with beautifully rendered fonts and a UI that supports multiple panes from the very first launch. The new branding looks excellent, and while there are still a few rough edges where the old themes haven't quite been replaced, Pulsar already feels like its own project. There's context-sensitive help, a file system browser, a built-in package manager for plugins, and smart autocompletion. The old packaging system was closed source, and while Pulsar can still access and use the old Atom.io package repository, the intention is to replace it with a new one containing open source package equivalents. Everything else is as it was in the original editor, and Pulsar means you can continue using your old configuration and project files with your own projects. Better yet, it's now in the hands of a community who are free to take the editor into completely new and untested directions, which is where Pulsar could really start to shine.

![](img/e3f454b04d121b3b3750fddfda8dd21e_84_2.png)

If you loved the Atom text editor, you'll equally love the open source and community-supported Pulsar fork.

**Project Website**
https://pulsar-edit.dev

### Code editor

## Open Komodo IDE

For over 20 years, the Komodo IDE was a proprietary development environment that worked best with web-related programming languages, including Python, PHP, Perl, Go, Ruby, Node.js, and JavaScript. It was published by ActiveState and went through three different teams, migrated through three different version control systems, and contributed to Mozilla's XPcom framework. It even managed to survive for years after the framework it was itself built on, XUL and XULRunner, were dropped by Mozilla back in 2016. But in late 2022, ActiveState finally decided to retire Komodo IDE and, fortunately, make it open source at the same time, creating the Open Komodo IDE project from its 3.2 million lines of code. This was a brilliant thing to do, and it's something that ActiveState has some history with after previously releasing its editing component, Komodo Edit, some time ago.

None of this would be important if the Komodo IDE weren't worth your time, and Open Komodo is going to be a brilliant option if you've not yet found your perfect IDE – especially if you use Python. It's obviously a mature and stable application with the open source version continuing from the release of Komodo IDE 12. It will feel familiar to anyone who has used Visual Studio Code, because the main window is split into various panes for listing files, methods, and symbols, with a central tabbed editor in the middle. All of this is configurable, and the editor is absolutely fantastic. There's syntax highlighting, code completion and built-in refactoring, visual debugging, and integrated version control. Maybe it's the K in its name, but it integrates very well with KDE, and the editor is very reminiscent of Plasma's Kate editor. If you're working with HTML or Markdown, there's a live preview of the renderer output of your work, which makes it particularly useful for working with projects with large documentation sets – something often neglected by most IDEs.

![](img/e3f454b04d121b3b3750fddfda8dd21e_85_0.png)

Komodo IDE is now open source and entirely dependent on its brilliant community for updates and builds.

**Project Website**
https://github.com/ActiveState/OpenKomodoIDE

### Networking monitoring

## Sniffnet

Thanks to the inbuilt capabilities of the Linux kernel, we're fortunate enough to have several high-profile and highly sophisticated network-monitoring tools. Wireshark has become an industry standard for low-level analysis, and higher level applications such as Pomerstear give us complete control over what goes into and out of our networks. But for non-experts, there isn't much choice. And for those people, Sniffnet could be enough. Sniffnet is a graphical network monitor that shows a pie chart of outgoing and incoming data alongside a breakdown of which networking protocols are being used. To start with, you need to select a network device detected on your system, and you need to run the application as root for adequate access permissions. You can also choose whether to monitor IPv4, IPv6, or UDP protocols, or all three, and there's an additional filter for specific network application protocols. Click on Run and the monitoring starts. It can help if the machine you're monitoring acts as a router, such as a server running Pihole, but it's also very interesting on a single machine because you can quickly see just how many protocols you use with normal network access. HTTPS will normally top the list, followed closely by the Simple Service Discovery Protocol (SSDP). Type ssh to connect to a remote machine, and you'll see SSH appear in the list of used protocols. Individual connections appear below, sorted optionally by most recent, most bytes, and most packets. The UI is simple and well suited to terminal-only rendering, a feature that's hopefully being worked on. Clicking on the Open full report button will output a full connection report to a text file. Even without augmentation, Sniffnet already offers a powerful and intuitive set of network monitoring features that will help the majority of us understand our own network traffic and see what's being used.

![](img/e3f454b04d121b3b3750fddfda8dd21e_85_1.png)

Sniffnet is easily installed via Cargo or DEB packages and, while the UI is simple, it does offer light and dark modes of rendering.

**Project Website**
https://github.com/GyulyVGC/sniffnet
