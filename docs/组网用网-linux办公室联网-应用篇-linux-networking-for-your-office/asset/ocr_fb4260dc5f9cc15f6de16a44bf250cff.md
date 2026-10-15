On the other hand, applications that are heavy on graphics, such as image editors and animation programs, may perform quite slowly, and perhaps even unacceptably slowly on some networks. This poor performance is due to the fact that the entire image data must be transmitted over the network. In some cases you might be able to improve performance by reducing the number of colors used by the X server, thus reducing the network load. Similarly, reducing the size of the displayed image might help.

# Tip

Programs and files that produce a dynamic display can chew up network bandwidth. For instance, many Web pages have animated graphics that change in a regular pattern. Although these files need to be transmitted from the hosting Web site to the computer containing the Web browser only once, the animation produces constant local network activity when you view such a page via a networked X server. To improve matters you might be able to disable animations, or all graphics, in your Web browser, or turn off animation options in other programs that use animation.

If you have a substantial need for remote X services but find that your network isn't fast enough, you might want to look into upgrading your network hardware. For instance, if you're using 10BaseT networking connections, upgrading to 100BaseT might improve network X performance substantially. (See Chapter 1, "Networking Hardware," for a discussion of network speed issues.)

# Using VNC

In practice, VNC is quite similar to a traditional remote X server configuration, but VNC does its work in a very different way. Rather than run the X server on the machine near you, VNC is an X server that runs on the host computer. On the machine you use, you run a relatively simple VNC client program. The VNC X server sends bitmap images of the screens to be displayed to the VNC client. The bitmap transmission means that VNC typically consumes more network bandwidth than does a traditional remote X server configuration, although this might not always be the case, depending on the applications in use.

VNC has two major advantages over a conventional X setup:

+   - VNC can be used to control a Windows computer remotely. You can even run a Windows computer from Linux by using VNC. Of course, you can mix VNC and traditional networked X servers on a single network, and even on a single computer, to meet your specific needs,