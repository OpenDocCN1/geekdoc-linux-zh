If the server serves mostly static HTML pages, chances are good that your CPU will not be a significant performance factor. On the other hand, if you generate a lot of dynamic content using Server-Side Includes (SSI), CGI scripts, and so on, your Apache server is likely to make good use of a fast processor. In such a case, getting a faster processor is advisable.

How fast is fast enough? There is no such thing as fast enough: The faster, the better! You should know, however, that just getting a fast CPU won't do you any good if you deal with a high volume of dynamic content. The most likely candidate for a performance bottleneck in such a scenario is RAM (discussed in the next section).

# ## RAM

You can never have enough RAM, but RAM costs money. The question then becomes how much RAM is going to give you the best performance for the money? You can answer this question by monitoring your system on a regular basis during load. For example, on most Unix systems, you can run utility programs to monitor your system performance. Figure 22-1 shows the output of one such widely available Unix utility called `top`.

![](bbox=[0.17, 0.49, 0.71, 0.71])

**Figure 22-1**: Output of the `top` program

A program such as `top` shows a great deal of information about a running system. In this particular sample output, the computer is using almost all of its physical memory (256MB), but has not yet used any of its virtual memory.

> **Note**  
> If you are running Apache on a Windows platform, use the Task Manager program to monitor memory, virtual memory, and CPU usage.