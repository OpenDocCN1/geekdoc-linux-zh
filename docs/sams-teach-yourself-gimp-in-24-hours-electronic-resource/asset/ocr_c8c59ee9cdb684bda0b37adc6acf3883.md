processors (not everyone runs Linux or uses an Intel processor), and it makes for easy
patching and bug fixing in the public arena. Trust me, compiling is a good thing, and
even the non-coding newbie get the hang of it after a few trials.

# Installing the Easy Way

After you have the source downloaded, you can begin compiling. As mentioned earlier,
GIMP provides a remarkable tool for accomplishing called gimp-tool. You can use this
tool to compile and install the plug-in only if the source has one .c file. This applies
to most of the simple filters you will encounter. Of course, you should read
the READMEs that come with any source distribution, but the procedure is usually as
:

+   - tar -xvf foo.plugin.tar.gz (compress)
- cd foo (cd directory)
- gimptool --install-admin foo.c (compile and install)

gimptool takes care of compiling, installing, and relocating the plug-in for you. The pre-
ceding example illustrates the steps to install a plug-in system-wide, which
should be done as route. Otherwise, if you want to install the plug-in locally only in your
own.gimp/plug-ins directory (not system-wide) all you need to give gimptool
--install argument. For any other functionality, the gimp help page should give
you the answers you need.

If the plug-in is more complex, that is, has many c source files, makefiles,
and so forth, you will need to take a more traditional installation route.

# ./configure && make && make install

If you're familiar with UNIX, the preceding headline phrase should be a mantra for
by now. One thing you should know is that your binary is compiled and relocated,
on the next startup GIMP registers the plug-in in your local pluginrc, which is
way the GIMP keeps track of which plug-ins are available and their preferences. It is
located in your .gimp directory (.gimp/pluginrc). The system-wide one, of course, is
installation-dependent, but is traditionally in /usr/share/gimp/1/. However, you should
ever find that one of your plug-ins is acting weird, deleting this file in your
local directory will fix it. GIMP will automatically create a new one on startup). In any
case, editing this file is probably not a good idea.

When installing complex, involved plug-ins with one source file, there is
really only one rule: Read the README and INSTALL documents, and follow the direc-
tions. Depending on the author, the documentation can range from informative to terse