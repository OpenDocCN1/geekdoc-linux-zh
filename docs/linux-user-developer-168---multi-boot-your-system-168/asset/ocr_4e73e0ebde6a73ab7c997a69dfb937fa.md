![](bbox=[0.09, 0.11, 0.43, 0.27])

# distcc

unpackaged and compiled, it is now actually ready to run – meaning you're done.

As long as the process completes without errors, you'll be able to launch the software on your Raspberry Pi; if you're developing for another platform (for instance, Android) then naturally with the software now compiled, you'll need to take steps to test it in a suitable environment.

# 16 Checking for errors

However, saying that, not every compiling task goes to plan. In situations where the compiler throws up error messages, you're going to need to be proactive to find out just what these errors mean.

This might be easier said than done, but if you're new to compiling, it's a good idea to have a pen and paper handy for jotting down error codes, and a browser window open to check them in Google. Remember to cross reference with the fact you're using distcc.

# 17 Make use of redundant hardware

With distcc we can take advantage of Linux devices that aren't doing anything, or have plenty of resources free to share. This is a pretty big deal; one that actually enables us to run miniature distributed cross-compiling networks in our own homes.

Whether you use a group of Pis for this, or simply tap into the spare resources of a desktop computer, it's a great way to use the Raspberry Pi.■

# Can I use this daily?

Quite often you'll find that Raspberry Pi projects are pretty cool, but they don't suit being done repeatedly on the little device. Like a proof of concept, such projects can inspire you to find out more, or offer a means to try something out (such as stop motion photography, for example) before you buy a dedicated device to use.

Distributed cross compiling, however, is not one of those things. Once you have it installed you can use this method again and again to save time.

# 14 Compile software with distcc

We're finally there. When you're ready to commit to compiling the application, enter the command:

```
`make -j8`
```

Then sit back and enjoy a cup of coffee. In the case of MAME, a single Raspberry Pi takes around 90 minutes to compile, but with a distcc in operation and the resources of a more powerful machine to rely on, we did it in 25 minutes!

# 15 Run your software

With the software now being completely downloaded.

![](bbox=[0.0, 0.48, 0.98, 0.98])