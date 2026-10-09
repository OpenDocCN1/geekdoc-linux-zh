# # Speeding Up Apache

If I were asked to write the simplest mathematical formula for performance, I would write Performance = f(hardware, software, network, content), which in English means that performance is a function of hardware, software, network, and content. Although this is a very broad statement, it highlights that performance of a Web server cannot be improved without ensuring that your hardware (that is the server computer), software (Apache server, Web applications, operating system), network (bandwidth, latency), and content (size, type) are tuned.

This chapter discusses how to tune these aspects of performance so that you can improve overall system performance.

# ## Using High-Performance Hardware

Apache runs on a variety of computers. Although the architecture may vary greatly, the hardware components that cause performance bottlenecks are virtually the same.

![](bbox=[0.12, 0.69, 0.22, 0.73])

By the way, because you're reading a chapter on performance, I assume that your current Apache system is a modern machine. If you told me that you use a PC clone as your Web server and were concerned about performance, I would assume that you have a Pentium class computer and not an i386-based system.

# ### CPU

When analyzing your hardware performance needs, the very first question you should ask yourself is this: “Do I need a fast CPU for my Apache computer?” The answer depends on how you use your Apache server.

# #### In This Chapter

+   - Benefiting from high-performance hardware
+   - Tuning your hard drive
+   - Tuning file systems
+   - Compiling and installing a custom kernel
+   - Tuning your network
+   - Tuning your Apache configuration
+   - Caching for speed
+   - Tuning Perl based Web applications