# ## Chapter 2

# # Graphics Basics

**Key Topics:**
* VGA cards
* Monitors
* Screen modes
* Resolution
* Color
* Video memory
* Compilation

By now you're probably wanting to do some coding, but we've got one more chapter to go through first. If you're desperately seeking the SVGAlib equivalent of "Hello, World", you can go ahead now and jump forward to Chapter 3. However, novices take heed: The material presented here will definitely clarify the exercises you'll encounter later. With that in mind, it may be wise to read this chapter first. The choice is yours; proceed accordingly.

Still here? Good. In this chapter, I'm going to give you a crash course covering the basics of computer graphics. You've got to crawl before you walk, after all. Learning the mechanics involved in producing graphical output will make your SVGAlib experience considerably easier. You'll see how VGA cards (and their variants) work together with your monitor to create images. From there, I'll discuss the various graphics modes, including the respective advantages and drawbacks of each, leading us into the concepts behind screen layout. Also, periodically, you'll encounter some terms that you'll need to know later in this book, such as D/I/A conversion, resolution, and acceleration.

> **Note**
> Not everything in this chapter will be SVGAlib specific, but don't be concerned. Because more than one operating system (OS) uses the Intel/Cyrix/AMD platform, it's not surprising that many x86 graphical programming elements are similar as well. If anything, this community will make life easier on people who are coming to Linux/SVGAlib from another OS, who may have already acquired some graphics experience.