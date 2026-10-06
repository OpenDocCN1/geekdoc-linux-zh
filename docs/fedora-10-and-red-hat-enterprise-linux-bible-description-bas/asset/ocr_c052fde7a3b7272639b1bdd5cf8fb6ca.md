to. With the text selected, select Text → Text and Font to see a window where you can choose the font family, font style, layout, and line spacing.

+   **Add graphical elements**—From the toolbar on the left, select the rectangle, 3D box, circles, start, or swirls. Move the cursor to the place where you want the new element, click and hold the mouse on that place, and move the mouse so the element grows to the size you want. Click the color palette on the bottom of the screen to change the element's color.

+   **Add clipart**—If you opened the clipart gallery, you can import clipart from there. Select File → Import and browse the /usr/share/clipart/openclip folder. Choose from hundreds of SVG clipart images in categories such as food, geography, recreation, and transportation. Once the image is imported, use your mouse to select and import as you did with the text

+   **Group objects**—Select a text or clipart object, hold the Shift key and select other objects. When all the objects in your group are selected, choose Object Group. You can now move all the objects around as one unit.

+   **Use layers**—Select the Layer to add, delete, raise or lower layers.

When you are creating your graphic, you can print that graphic by selecting File → Print. From the printer window, you can select the image in vector or bitmap format from the Rendering tab.

# # Using Scanners Driven by SANE

Software for using a scanner for Linux is being driven by an effort called Scanner Access Now Early (SANE). This effort hopes to standardize device drivers for equipment such as scanners, digital cameras, and digital video cameras are created, and also help simplify the interfaces for applications that use those devices.

SANE is known for the Fedora and RHEL distributions. The sane-backends, sanefrontends, xsane, and sane-gimp packages are all on the DVD that can come with this book. You can get the latest SANE driver packages from http://www.sane-project.org.

Someone wanting to use Linux as a publishing platform is generally interested in those two issues about scanners: which scanners are supported and which applications are available to use the scanners. In the past, most scanners have been supported under parallel scanners. However, have given way to the more convenient USB scanners.

Because of the ongoing effort, new scanners are being supported all the time. You can find a current list of supported scanners at http://www.sane-project.org/sane-supported-devices.html. For applications, these are currently available with Fedora and RHEL:

+   This is an X-based graphical front for SANE scanners; xsane can work as a GIMP plug-in or as a separate application. (From The Applications menu, select