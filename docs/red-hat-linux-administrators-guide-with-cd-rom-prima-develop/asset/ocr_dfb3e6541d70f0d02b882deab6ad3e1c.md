equivalent to issuing a “shutdown” command while the latter is equal to a “reboot” .

# # Running Program Specific Scripts

Sometimes you will want to install programs that will need to boot up automatically in case of a reboot or power failure. You might not always have access to the machine when it first comes back up, so you want to make sure that your program starts up by itself. In cases like these where there is no RPM or binary version of the program and you are compiling the executable from source, you will need to create a customized script.

If you lack a broad understanding of how to create a bootup script, you can usually copy an existing script and then modify it for your own use. This, however, is not a foolproof method, especially if you lack experience in programming languages. Another way is to create a very simple script that accomplishes the same means of starting up but without all the extraneous options or commands typical of other scripts.

For an example this time, let’s use the Apache Web server. You can install the RPM version of Apache on most any Linux box running Red Hat, which in turn installs all the startup scripts. However, you might want to compile the source code yourself to optimize some of the more advanced modules or simply to try your hand at compiling source. There are advantages to both methods, which won’t be examined here, but both also have their disadvantages. For more information on compiling programs from source, see Chapter 11, “Installing Additional Programs.” This chapter also discusses the difference between using both source and binary programs under Linux.

After successfully compiling and executing the program you will want confirm that should the machine lose power and need to be rebooted or if for some other reason it needs assistance in restarting, the web daemon will restart as well.

Here is a sample script that you can place in the `/etc/rc.d/rc3.d/` directory. It is called S99apache. The initial character needs to be capitalized so that the bootup will recognize it. If you want to disable this function y keep the script, merely change the capital S to a lowercase s. The letter S signifies starts, while the other initial letter, K, denotes kill and is used to shut down certain daemons. Listing 2.5 shows how this simple script starts the web daemon.