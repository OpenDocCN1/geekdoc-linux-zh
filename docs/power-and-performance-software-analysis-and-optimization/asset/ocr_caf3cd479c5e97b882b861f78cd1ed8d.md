# 10.1 Traditional graphics stack 181

As a result, Xlib function calls are blocking, meaning that they don't return until
t associated request's reply has returned from the server. Obviously, this can be
less desirable than if the request's reply isn't needed immediately. The XCB library
addresses this problem by exposing more of the protocol, and allowing the application
dec whether to block. Most modern applications do not utilize these libraries
directly, but instead leverage tools GTK or Qt, which in turn use Xlib or XCB.

While the protocol provides the functionality for window management, this
is only applicable to the window as a canvas for drawing. These
drawable canvases are known as pixmaps. Other common window elements, such as
t window's placement, decorations, including the title bar and minimize, maximize,
close buttons, or behaviors as resizing a window when the border is dragged,
not controlled by the X protocol. These elements fall into the purview of the
window manager. Which is a server client just like the windows it manages.
The window manager is responsible for rendering each of the windows, both their
content and decorations, and composing into one image for display on the screen, that is,
posing the various windows. As the reader might, rendering each window
to an internal buffer and then composing additional overhead that can be
detimental to performance-sensitive tasks. Due to this, most high-quality window
managers disable disabling when an application runs in fullscreen mode, thus
igating the performance overhead.

While many users prefer to only utilize a window manager on top of X, such as
OpenBox, Fluxbox, Razpoint, or dwm, others choose to utilize a full desktop
environment, such as gnome or KDE. Each desktop environment includes a win-
dow manager, such as Metacity and Kwin for GNOME and KDE respectively, but also
additional software for greater functionality; Most desktop environments can
be configured to use a different window manager, if desired.

# 10.1.2 HARDWARE AND LOW-LEVEL INFRASTRUCTURE: DRI

Designed in 1984, of the functionality within the X protocol has outlived its
fulness. This is why the Wayland protocol, which is architected for the needs of
modern graphics applications, is her presumptive to the future Linux graphics
stack. At the time the X protocol is still in use, in order to get
acceptable performance, the stack essentially bypasses the X server at all
costs. This occurs through the Direct Rendering Infrastructure (DRI), which enables
graphics applications to skip the X interface and interact directly with the
hardware. This infrastructure is divided into three different kernel components: DRM,
GEM, and KMS.

The Direct Rendering Manager (DRM), allows for user applications to submit
code to the GPU, without involving the X server (Barnes et al., 2012). The
interface for the DRM infrastructure is exposed to user space through an API of
ioctl(2) calls, performed on the GPU's DRI file descriptor. These special DRI
device files can be found under /dev/dri. In order to simplify this process, the
ict(2) calls in user space are typically handled by a helper library, libdrm.