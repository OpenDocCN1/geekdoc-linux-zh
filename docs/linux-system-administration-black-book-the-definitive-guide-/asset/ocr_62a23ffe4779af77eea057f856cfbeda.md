![](bbox=[0.0, 0.08, 0.11, 0.25])

To get the most out of the post-installation possibilities, spend some time getting familiar with shell scripting (covered in detail in Chapter 20). Depending on your skill level, you can do many things with this section that will help you to avoid having to duplicate configuration steps as you complete the installs on all of your machines.

# # The Test-Edit Cycle

You will hear much about the Test-Edit-Compile cycle later in this book, when we get to shell scripting and Perl and C programming. This cycle applies to any instance in which you want to ensure that the file you prepared instructs the computer to do exactly what you want it to do. Remember the old phrase “garbage in, garbage out”? Sometimes, our imprecise human nature confuses computers terribly.

A KickStart install automation file has only two steps: test and edit. You don’t need to compile anything here. Adding the word “Test-Edit” to the title indicates that this procedure is not something you do just once. You have to repeat this set of processes until you finally get the result you are looking for. Sometimes this process ends quickly, but other times it is frustrating and tedious. However, if you want your machines installed properly so you do not have to go back and fix all of them, then follow this process faithfully.

In the case of preparing an automated installation, the various pieces of this cycle are covered in different sections of the Immediate Solutions section. Start with the section “Installing The First Machine.” After all, your KickStart results rely on how that first machine is handled.

After the first machine is up and running, do not proceed to what you might usually do—in other words, do not start setting things up! Treat bulk installs such as this as a multiphase process. The Test-Edit cycle is just one phase in the beginning of the process. In fact, it is a phase you have not even entered yet. Next, you need to look at the section “Building The Initial KickStart File,” which provides the instructions for making the file that automates the rest of the installs. After you prepare this file, you are ready to start the cycle.

As the cycle’s name suggests, the first thing you might do is test your current KickStart script. However, the first time, you are recommended to go straight to the Edit phase. Sometimes, the file is not generated exactly right and needs a bit of tweaking. The earlier section “The Structure Of A KickStart Script” should be of great help when you’re reviewing your new script. Make sure that everything is correct, and then return to the beginning of the cycle, back to Test.

Choose one of the machines that you intend to set up as a clone of the first machine, and then turn to the Immediate Solutions section “Installing With KickStart”