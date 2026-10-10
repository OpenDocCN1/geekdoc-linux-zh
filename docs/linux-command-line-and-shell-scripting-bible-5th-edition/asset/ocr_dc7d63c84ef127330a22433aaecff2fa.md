# # Managing Filesystems

# CHAPTER

# 8

+   **IN THIS CHAPTER**
+   
+   * Exploring Linux filesystems
+   * Working with filesystems
+   * Managing logical volumes

**W**hen you're working with your Linux system, one of the decisions you'll need to make is what filesystem to use for the storage devices. Most Linux distributions provide a default filesystem for you at installation time, and most beginning Linux users just use it without giving the topic another thought.

Although using the default filesystem choice isn't necessarily a bad thing, sometimes it helps to know the other options available to you. This chapter discusses the different filesystem options you have available in the Linux world and shows you how to create and manage them from the Linux command line.

# ## Exploring Linux Filesystems

Chapter 3, “Basic Bash Shell Commands,” discussed how Linux uses a *filesystem* to store files and folders on a storage device. The filesystem provides a way for Linux to bridge the gap between the ones and zeros stored in the hard drive and the files and folders you work with in your applications.

Linux supports several types of filesystems to manage files and folders. Each filesystem implements the virtual directory structure on storage devices using slightly different features. This section walks you through the strengths and weaknesses of common filesystems used in the Linux environment as well as some history regarding them.

# ### Exploring the Linux filesystem evolution

The original Linux system used a simple filesystem that mimicked the functionality of the UNIX filesystem. This section discusses its improvements through time.