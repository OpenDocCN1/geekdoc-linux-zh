# Exercise 14-1    AppArmor

In this exercise, you create, test, and improve a profile for the Firefox browser. This exercise has four parts.

In the first part create a profile for the Firefox browser. While using Firefox to generate log entries for the initial profile, just surf the web; do not access local files with Firefox.

In the second part, use Firefox to access a local file, such as /usr/share/doc/packages/apparmor-docs/apparmor.7.html. AppArmor should prevent you from viewing the file. Change the profile to allow access. You could use YaST, genprof, or complain and logprof for this purpose.

In the third part, install the Java browser plug-in package java-1_4_2-sun-plugin. Restart Firefox and use it to access a page containing a Java applet.

http://java.sun.com/products/plugin/1.4/demos/plugin/applets.html links to various demos. Firefox will not be able to show these. Change the profile again to be able to run Java applets. Use another method to do so than the method used in part two above.

In the fourth part, compare the profile you generated with those in /etc/apparmor/profiles/extras/ for Firefox. Find out if your profile is more restrictive or more permissive compared with those profiles.

# Detailed Steps to Complete this Exercise

+   Part I: Create a Profile for the Firefox Browser

+   Part II: Modify the Profile for Firefox to Allow Read Access to the Local File System

+   Part III: Use a Browser Plug-in

+   Part IV: Compare the Profile You Created with Those From SLES 10