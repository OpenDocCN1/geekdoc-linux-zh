options to enable the use of an external monitor. For example, NeoMagic chipset users might need to use the following:

```
option    “extern_disp”
option    “intern_disp”
```

These options, included in XF86Config’s *Device* section, will enable the use of the LCD and external monitor at the same time. You can generally expect to be able to use a greater screen resolution with an external monitor, but this is not always the case. You’ll need to experiment with an external monitor to arrive at the best settings.

# **Multithread? Xinerama?**

Notebook users probably won’t be able to use the LCD and external monitor as a single monitor, even with the release of the new version 4.0 of XFree86. Although X11 supports this feature, multithread displays are generally hardware-dependent and require a compliant graphics card. The Xinerama feature, although supported by XFree86, requires a compliant or Xinerama-aware window manager—a feature not yet supported for Linux.

# # Resource Information

+   *   `http://www.gnu.org/software/bash/bash.html`
+       *   The starting point for learning about and downloading the latest version of the GNU bash shell.
+   *   `/usr/doc/bash-doc*`
+       *   A mother lode of online technical information about bash.
+   *   `http://sunsite.auc.dk/zsh/`
+       *   The home page for the zsh shell.
+   *   `http://www.oase-shareware.org/shell/articles/ignorantsguide.html`
+       *   Heiner Steven’s collection of shell programming articles. A good collection of tips and hints for getting started with shell programming.