These steps help you prepare your Fedora Core computer to start building the multimedia server:

+   1. Log in to your computer as any user.

+   2. Open Mozilla, go to www.icecast.org, and click the Download link at the top of the page.

Now you have to download the icecast2 and ices2 software from the Internet.

+   3. Click the icecast-2.0.2.tar.gz link.

A dialog box labeled Opening icecast-2.0.2.tar.gz opens.

+   4. Click the Save it to disk option and then click the OK button.

A dialog box labeled Enter name of file to save to... opens.

+   5. Click the Save button.

The file is downloaded to your computer.

+   6. Back in your browser, scroll down the page and click the libshout-2.0.tar.gz link.

The Enter name of file to save to... dialog opens.

+   7. Click the Save button and the libshout archive file is downloaded to your computer.

+   8. Once again, back in the www.icecast.org Web page, click the Ices link at the top, right of the page.

The Ices download page opens. Now it's time to download the ices2 source code.

+   9. Click the ices-2.0.0.tar.gz link.

A dialog box labeled Enter name of file to save to... opens.

+   10. Click the Save button.

The ices2 file is downloaded into your current directory.

Note that in this section, we break our unstated rule of installing only pre-compiled software from RPM packages. Although Icecast2 is available in RPM format, ices2 is not. We could use the Icecast2 package, but it requires a library (software that's shared between many programs) that's difficult to find. Therefore, compiling Icecast2 and Ices2 from scratch turns out to be easier. (It's also fun to know how we nerds spend our Saturday nights!)

Before installing Icecast2 and Ices2, we have to install the libshout libraries:

+   1. Open a terminal window by clicking the GNOME Menu and choosing System Tools:: Terminal.

These instructions assume that you're working from your home directory.