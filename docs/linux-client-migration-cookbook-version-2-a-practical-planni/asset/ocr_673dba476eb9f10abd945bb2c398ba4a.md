# Python

Python is a modern object-average scripting language that has remarkable power while still maintaining clear syntax. There are built-in libraries, which provide abstractions for many platform specific features (such as file access and threading), and many built-in or third-party open source libraries for graphical applications (such as PyGTK, PyQt, and wxPython, and bindings for Mac OS X and Microsoft Foundation Classes (MFC)). New modules can be written in either Python, C, or C++. While an entire application can be written in Python, it is also frequently used as an extension language for applications that have a built-in plug-system

Red Hat uses Python extensively in the installation process and at many other places. Tools, such as kudzu (which is also used for hardware recognition in the Debian-based Knoppix distribution), are available as Python modules, too. While using **kudzu --probe** is straightforward, the Python wrapper allows administrators to write their own hardware recognition scripts in a much more elegant fashion, as seen in Example F-1

Example: F-1 Hardware recognition with kudzu and Python

```
#!/usr/bin/env python

kudzu
print kudzu.probe(kudzu.CLASS_SOCKET, kudzu.BUS_PCI, kudzu.PROBE_ALL)
print kudzu.probe(kudzu.CLASS_NETWORK, kudzu.BUS_PCI, kudzu.PROBE_ALL)
```

```
devices = kudzu.probe(kudzu.CLASS_UNSPEC, kudzu.BUS_UNSPEC, kudzu.PROBE_ALL)
for dev in devices: print dev
```

# Embedded Scripting Languages

Most Linux scripting languages have wrappers for the GTK+, Qt, and wxWidgets libraries, and the whole GK/GNOME APIs. It is possible to write simple desktop applications or panel applets in a scripting language in order to allow for rapid development. Several applications also have embedded languages, which allow for user-customized actions. Such customization is often useful to tailor these applications for your exact business needs. The language used for these embedded capabilities often varies by application. For example, Perl and Python are used in Gnumeric and The GIMP,

Appendix F. Desktop automation and scripting 323