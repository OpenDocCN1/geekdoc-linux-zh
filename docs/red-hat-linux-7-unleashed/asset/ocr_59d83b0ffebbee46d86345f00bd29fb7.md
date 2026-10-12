To install the new version of the `sendmail` executable, first stop the currently running daemon with the following command:

`[root@gonzo src]# /etc/rc.d/init.d/sendmail stop`

Then type this:

`[root@gonzo src]# ./Build install`

With everything in place, you can restart the new daemon with the following:

`[root@gonzo src]# /etc/rc.d/init.d/sendmail restart`

# # sendmail.cf: The Configuration File

With the advent of V.8, `sendmail` has shipped with a quick and easy way to automatically create a `sendmail.cf` file for you. In fact, it is highly recommended that you do *not* create or modify any `sendmail.cf` files manually. You can safely skip this section if you aren’t interested in the gory details regarding the `sendmail.cf` file. (I discuss the easy way to configure `sendmail` in the next section.)

The `sendmail.cf` file provides `sendmail` with its brains, and because it’s so important, this section covers it in fairly executing detail. Don’t worry if you don’t understand everything in this section the first time through. It will make more sense upon rereading and after you’ve had a chance to play with some configuration files of your own.

`sendmail`’s power lies in its flexibility, which comes from its configuration file. `sendmail.cf`. `sendmail.cf` statements compose a cryptic programming language that doesn’t inspire much confidence at first glance (but C language code probably didn’t either, the first time you saw it). However, learning the `sendmail.cf` language isn’t very hard, and you won’t have to learn the nitty-gritty details unless you plan to write a `sendmail.cf` from scratch—a bad idea at best.

# ## General Form of the Configuration File

Each line of the configuration file begins with a single command character that indicates the function and syntax of that line. Lines beginning with a `#` are comments, and blank lines are ignored. Lines beginning with a space or tab are continuations of the preceding line, although you should usually avoid continuations.

Table 10.1 shows the command characters and their functions as well as an example of their usage. This table is split into three parts corresponding to the three main functions of a configuration file, which are covered later in the section “A Functional Description of the Configuration File.”