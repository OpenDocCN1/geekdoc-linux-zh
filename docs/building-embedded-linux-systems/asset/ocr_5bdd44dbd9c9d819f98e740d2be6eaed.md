Linux magazines now run embedded features on a regular basis. Indeed, one of the authors of this book was responsible for such a column for a number of years and still writes articles on occasion.

# Copyright and Patent Issues

You may ask: what about using Linux in my design? Isn't Linux distributed under some crazy license that may endanger the copyrights and patents of my company? What are all those licenses anyway? Is there more than one license to take care of? Are we allowed to distribute binary-only kernel modules to protect our IP? What about all these articles I read in the press, some even calling Linux's license a “virus”?

These questions and many more have probably crossed your mind. You have probably even discussed some of these issues with your coworkers. The issues can be confusing and can come back to haunt you if they aren't dealt with properly. We don't say this to scare you. The issues are real, but there are known ways to use Linux without any fear of any sort of licensing contamination. With all the explanations provided next, it is important to keep in mind that this isn't legal counsel and we are not qualified lawyers. If you have any doubts about your specific project, consult your company attorneys—that's what they're there for. Seriously, you want to figure this out now so that it's not a problem for you later; with a little understanding and forethought, it won't be.

# Textbook GPL

For most components making up a Linux system, there are two licenses involved, the GPL and the LGPL, introduced earlier. Both licenses are available from the FSF's website at [http://www.gnu.org/licenses/](http://www.gnu.org/licenses/) and should be included with any package distributed under the terms of these licenses.$^{8}$ The GPL is mainly used for applications, whereas the LGPL is mainly used for libraries. The kernel, the binary utilities, the gcc compiler, and the gdb debugger are all licensed under the GPL. The C library and the GTK widget toolkit, on the other hand, are licensed under the LGPL.

Some programs may be licensed under BSD, Mozilla, or another, but the GPL and LGPL are the main licenses used, but regardless of which one you use, common sense should prevail. Make sure you know the licenses under which the components you use fall and understand their implications. Also make sure you understand the “compatibility” of the licenses for different components that you may wish to use within the same project. Your attorney will be able to advise.

The GPL provides rights and imposes obligations very different from what may be found in typical software licenses. In essence, the GPL is meant to provide a higher degree of freedom to developers and users, enabling them to use, modify, and distribute

> $^{8}$ The licenses are often stored in a file called `COPYING`, for the GPL, and a file called `COPYING.LIB`, for the LGPL. Copies of these files are likely to have been installed somewhere on your disk by your distribution.