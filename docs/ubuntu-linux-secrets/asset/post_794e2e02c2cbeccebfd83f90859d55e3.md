
Click the Install Now button to install the Fast Video Download extension. When complete, the Add-ons dialog box appears, showing that the installation was successful.

- 4. Click the Restart Firefox button for the new extension to work.

When Firefox starts, you should notice a new icon on the right side of the bottom status bar. The Add-ons dialog box also appears, showing that the Fast Video Download extension has been installed properly, as shown in Figure 12-9.

![](img/39e65eeb4f54001ede08c6114ae3cc6c_336_0.png)

Figure 12-9: The Fast Video Download extension installed.

To use Fast Video Download, navigate to a web page that contains an embedded streaming video, then click the New icon in the status bar. Fast Video Download scans the web page looking for the video links, then displays a dialog box asking you where to save the file.

## Editing Videos

Along with the popularity of digital cameras that can record video comes the popularity of video-editing software packages. Unfortunately, Ubuntu doesn't install a video-editing package by default. However, if your workstation is connected to the Internet, it's a snap to install a basic editing package.

The Kino video-editing package is the most popular video editor for the Linux platform. It uses a subtractive method of video editing, meaning that you add video clips to a library then remove the pieces that you don’t want to use in your final video. This is a little more basic than what some advanced video editors allow you to do, but it should work just fine for most home-video enthusiasts.

This section describes how to install and use the Kino video-editing software in Ubuntu.

## Installing Kino

Although Ubuntu doesn’t install Kino by default, it does provide an easy installation package. You can install Kino from the Synaptic Package Manager (see Chapter 13). Just follow these steps to install Kino on your workstation:

- 1. Open the Synaptic Package Manager by selecting System ◄ Administration ◄ Synaptic Package Manager from the top panel. For details on how to use the Synaptic Package Manager, see Chapter 13.

- 2. In the Quick Search text box, enter the term kino. The search results appear in the software list window on the right side of the Package Manager, as shown in Figure 12-10.

- 3. Click the Kino package and select the Mark for Installation option from the popup menu.

![](img/39e65eeb4f54001ede08c6114ae3cc6c_337_0.png)

Figure 12-10: Finding Kino in the Package Manager package list.

4. Click the Apply button from the top toolbar. The Package Manager will display a dialog box confirming your decision to install the new software package.

5. The Package Manager downloads and installs Kino, then produces a dialog box indicating that the installation is complete. Click the Close button to exit the installation.

Once you've installed Kino it'll appear in the top panel, under Applications ▸ Sound & Video ▸ Kino. Select that entry to start Kino. The main Kino window, shown in Figure 12-11, appears on the desktop.

![](img/39e65eeb4f54001ede08c6114ae3cc6c_338_0.png)

Figure 12-11: The main Kino window.

Now you're ready to start your video editing!

## The Kino Interface

The Kino window consists of several elements:

- The menu bar: Provides access to all of the modes and editing features.
- The toolbar: Provides buttons for quick access to common editing features.
- The storyboard: Displays individual clips from a video for selecting and removing from the video file.
- The mode pages: Provides options for the specific editing mode used.
- The scrub bar: Allows you to seek within the movie by dragging the arrow pointer.
- The transport controls: Controls playback and fast seeking through the video file.

The mode pages are the key to Kino. Each mode page provides a different editing interface for interacting with the individual video clips in the video file. Six mode pages are available and are described in Table 12-2.

## Table 12-2: The Kino Mode Pages

| Mode Page | Description |
|---|---|
| Edit | Displays the video clip segment. You can use Edit mode to move clips around in order and remove clips from the storyboard. Once you rearrange the clips you can view the result in the Edit mode window. |
| Capture | Selects an external device from which to capture video. You can record the video captured from the external device to make new clips in the storyboard. |
| Timeline | Displays the video clips along with timestamp information, showing the relative times for each clip in the storyboard and how they contribute to the overall time of the video. |
| Trim | Provides basic cut-and-paste features within the video clips. You can use Trim mode to insert and remove clips from the video. |
| FX | Adds basic special effects to the video, such as blur, pixilation, flips, and changing colors. |
| Export | Allows you to output the current video to another format or device. |

As you can see from its modes, Kino has a long way to go before it becomes a professional-quality video-editing tool, but it does provide a basic video-editing environment for working on simple video files.

## The Kino Preferences Settings

You can reach the Kino Preferences window by clicking Edit ▸ Preferences from the menu bar. The Preferences window is shown in Figure 12-12.

The Preferences window uses seven tabs to organize the various settings you can make:

- Defaults: for controlling the video and audio defaults:
  - Normalisation: Select NTSC or PAL video modes.
  - Audio: Select the default audio sampling rate.
  - Aspect Ratio: Select 4:3 full-screen or 16:9 widescreen formats.
- Capture: for controlling the settings for saving captured video:
  - File: Specify the default filename to store captured video.
  - File Type: Select AVI type 1, AVI type 2, or OpenDML AVI video format for storing the video.
  - Other File Options: Select file details such as how often to write frames to the file, whether to use the timestamp in the filename, and how to split the capture into multiple files.
- IEEE 1394: for specifying which IEEE 1394 (FireWire) device to capture from.
