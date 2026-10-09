# **Error recovery**

In case a problematic situation occurs, it is expected that the program will take steps to recover cleanly from the problem condition and then alert the proper authorities (perhaps a system administrator or the owner of the device running the software in question) with a meaningful diagnostic message.

# *Longevity*

The program will run unassisted for long periods of time and will conserve its integrity, regardless of the situations it encounters. The program cannot fail simply because a system logfile became too big (something one of the authors of this book admits to having once learned the hard way).

Most programmers agree that the Linux kernel and other projects used in a Linux system fit this description of quality and reliability. The reason is the open source development model (see upcoming note), which invites many parties to contribute to projects, identify existing problems, debate possible solutions, and fix problems effec-tively. Poor design choices are made from time to time, but the nature of the develop-ment model and the involvement of “many eyeballs” serve to more quickly identify and correct such mistakes.

These days you can reasonably expect to run Linux for years unattended without prob-lems, and people have effectively done so. You can also select which system compo-nents you want to install and which you would like to avoid. With the kernel, too, you can select which features you would like during build configuration. As a testament to the quality of the code that makes up the various Linux components, you can follow the various mailing lists and see how quickly problems are pointed out by the individ-uals maintaining the various components of the software or how quickly features are added. Few other OSes provide this level of quality and reliability.

![](bbox=[0.17, 0.62, 0.25, 0.71])

Strictly speaking, there is no such thing as the “Open Source” develop-ment model, or even “Free Software” development model. “Open source” and “Free Software” correspond to a set of licenses under which various software packages can be distributed. Nevertheless, it remains that software packages distributed under “Open Source” and “Free Software” licenses very often follow a similar development model. This development model has been explained by Eric Raymond in his seminal book, The Cathedral and the Bazaar (O’Reilly).

# Availability of code

Code availability relates to the fact that Linux’s source code and all build tools are available without any access restrictions. The most important Linux components, in-cluding the kernel itself, are distributed under the GNU General Public License (GPL). Access to these components’ source code is therefore compulsory (at least to those users who have purchased any system running GPL-based software, and they have the right to redistribute once they obtain the source in any case). Other components are