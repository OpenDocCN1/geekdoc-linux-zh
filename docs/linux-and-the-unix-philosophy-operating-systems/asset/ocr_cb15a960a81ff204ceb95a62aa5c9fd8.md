Because GUI programs expect to communicate with a human being at some point, it's very difficult to incorporate them into shell scripts. It takes many lines in a shell script to carry on the kinds of dialogs that CUIs require. These dialogs can be so cumbersome to write in a shell script that programmers often resort to small user interface programs to conduct yes-no queries and obtain other responses from the user.

Since CUIs hinder interaction with other programs, they are typically used only for their original purpose and not much else. Although you might suggest that this is simply a case of "doing one thing well," a CUI differs from small Unix commands in that it exists as an application unto itself. It doesn't offer the same mix-and-match, plug-and-play features of its Unix counterparts. It yields very little in terms of software leverage as a result.

Without software leverage, CUI programs cannot multiply their effects-and the effects of their developers-on the computer world. Although a CUI program may gain an early following because of its novelty when it is released, it soon loses its appeal as the rest of the software world marches on. Software advances appear daily on the computer scene, and a few ideas cause major upheaval in each decade. The monolithic CUI program is simply incapable of adapting in such a rapidly evolving environment.

# 6.1.7 "Who cares about CUIs? Nobody types anymore."

Some of you may be wondering why there is so much discussion about CUIs in the first place. After all, aren't most user interfaces graphical these days? Why be concerned with typing things on the command line when you can view a list of check boxes and click on them with a mouse?

The short answer is that a GUI is simply a visual form of a CUI. Thus, it has the same characteristics as a CUI for the following reasons:

+   - It assumes that the user is human. The software designer expects that a physical user will be present to click on buttons and navigate menus. In some cases, steps are taken to slow the program down to better accommodate the user. Frequently, more effort is spent on making the user interface than on providing functional capabilities.

+   - A GUI is often big and difficult to write. Large IDEs such as Microsoft's Visual Basic and Borland's Jbuilder have ameliorated this problem somewhat. But these IDEs have problems of their own that we've explored elsewhere.

+   - GUIs tend to adopt a big is beautiful approach. If five options meet the need, then ten options meet the need even better. That's the rationale behind some office programs that have grown to gargantuan proportions. When you want to drive a couple of nails, you don't need to hire a construction company to come in with a team of laborers armed with nail guns.

+   - It's difficult to combine GUI-based programs with other programs. Unless the program has initially been designed to interface with another program, it won't interface well. In the Microsoft world, OLE and COM provide some of this connectivity. With most Unix and Linux commands, such interfaces are unnecessary,