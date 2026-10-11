# Preface

hen I was first approached about converting my experiences with the Linux kernel
into a book, I proceeded with repudation. What would place my book at the top of its
subject? I was not interested unless I could do something special, a best-in-class work.

I realized that I could offer a unique approach to the topic. My job is hacking the kernel.
My hobby is hacking the kernel. My love is hacking the kernel. Over the years, I have
accumulated interesting anecdotes and insider tips. With my experiences, I could write a
book on how to hack the kernel and-just as important-how not to hack the kernel. First and
foremost, this is a book about the design and implementation of the Linux kernel. This book's
approach differs from would-be competitors, however, in that the information is given with
a slant to learning enough to actually get work done-and getting it done right. I am a
pragmatic engineer and this is a practical book. It should be fun, easy to read, and useful.

I hope that readers can walk away from this work with a better understanding of the
rules (written and unwritten) of the Linux kernel. I intend that you, fresh from reading
this book and the kernel source code, can jump in and start writing useful, correct, clean
kernel code. Of course, you can read this book just for fun, too.

That was the first edition. Time has passed, and now we return once more to the fray.
This third edition offers quite a bit over the first and second: intense polish and revision,
updates, and many fresh sections and all new chapters. This edition incorporates changes in
the kernel since the second edition. More important, however, is the decision made by the
Linux kernel community not to proceed with a 2.7 development kernel in the near to mid-
term. Instead, kernel developers plan to continue developing and stabilizing the 2.6 series.
This decision has many implications, but the item of relevance to this book is that there is
quite a bit of staying power in a contemporary book on the 2.6 Linux kernel. As the Linux
kernel matures, there is a greater chance of a snapshot of the kernel remaining representative
long into the future. This book functions as the canonical documentation for the kernel,
documenting it with both an understanding of its history and an eye to the future.

# **Using This Book**

Developing code in the kernel does not require genius, magic, or a busy Unix-hacker
beard. The kernel, although having some interesting rules of its own, is not much different
from any other large software endeavor. You need to master many details-as with
any big project-but the differences are quantitative, not qualitative.

> ¹ This decision was made in the summer of 2004 at the annual Linux Kernel Developers Summit in
> Ottawa, Canada. Your author was an invited attendee.