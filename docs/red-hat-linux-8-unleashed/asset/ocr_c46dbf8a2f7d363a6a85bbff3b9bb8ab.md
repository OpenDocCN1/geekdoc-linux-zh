when contacted by the appropriate software, identify the appropriate CD and send the information to be displayed locally. Many CD player applications provide this functionality. The service is interactive. If you have a CD that isn't in the CDDB database, the Web site tells you how you can add the information to the database.

Each GUI application for burning CDs has different strengths and weaknesses. You should experiment with all the different graphical tools as well as try your at command-line burning, and you'll have a significantly richer multimedia experience with Red Hat Linux.

# Using KOnCD

KOnCD is a graphical client that you can use to copy a CD, make a data CD, make an audio CD, rip audio tracks from a music CD, or erase a CD-RW. The setup of KOnCD is straightforward, as shown in Figure 26.1, where root tells the application users has permission to access the CD device (access for removable media devices is usually restricted to root as a security measure). The permissions issue is important because new-user confusion and frustration over CD-RW arises from the lack of understanding of restrictions governing that use. The icons on the left are selected to set the default device and the default paths to the applications (all GUI CD applications are no more than front ends to coreg, mkisofs, and related commands).

![](bbox=[0.245, 0.493, 0.712, 0.695])

**Figure 26.1** An useful feature of KOnCD is the capability to add users to the group allowed to use the CD writer. KOnCD will automatically detect many, if not all, of the appropriate defaults.

After you've added the client's users, you can set up the image options (as you did with the options you added to the mkisofs command). The Image Type drop-down list displays the collection of predefined options (see Figure 26.2). You can choose advanced image options in the upper area of the window. Check an option to enable it; check the check box to turn the option off. When you've finished choosing options, click the Save button.