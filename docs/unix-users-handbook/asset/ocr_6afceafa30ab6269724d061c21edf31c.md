The shell is one of the most powerful features on any UNIX system. If you can’t find the right command to accomplish a task, you can probably build it quite easily using a shell script.

The best way to learn shell programming is by example. There are many examples given in this chapter. Some serve no purpose other than to demonstrate the current topic. Most, however, are useful tools or parts of tools that you can easily expand and adapt into your environment. The examples provide easy-to-understand prompts and output messages. Most examples show what is needed to provide the functionality we are after. They do not do a great deal of error checking. From my experience, however, it only takes a few minutes to get a shell program to do what you want; it can take hours to handle every situation and every error condition. Therefore, these programs are not very dressed up (maybe a sport coat versus a tuxedo). I’m giving you what you need to know to build some useful tools for your environment. I hope that you will have enough knowledge and interest by the time we get to the end of this chapter to learn and do more.

Most of the examples in this chapter were performed on a Solaris system; however, shells are nearly identical going from one system to another so you should be able to get the programs in this chapter running on your system quickly.

# ### Steps to Create Shell Programs

When you craft a shell program, there are some initial steps you want to perform so that you have consistency among all of your programs. The following is a list of some important concepts to employ with your shell programs:

+   1. **Names of shell programs and their output** - You should give your shell programs and their output a meaningful name. If you call your shell programs *script1, script2* and so on these will not have any meaning for you and other potential users of the programs. If your shell program finds files of a particular