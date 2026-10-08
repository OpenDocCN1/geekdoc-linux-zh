
# Work with Python

```bash
$ toast test/processOptions.py
$ ./processOptions.py processOptions.py
test
Copying to test/processOptions.py
test/processOptions.py already exists!
$ ./processOptions.py processOptions.py
test -n
Copying to test/processOptions.py
test/processOptions.py already exists!
$ ./processOptions.py processOptions.py
test -i
Copying to test/processOptions.py
test/processOptions.py already exists!
[y/n]: y
Copying processOptions.py to test/
processOptions.py
$ ./processOptions.py processOptions.py
test -i
Copying to test/processOptions.py
test/processOptions.py already exists!
[y/n]: n
Cannot override test/processOptions.py
```

Although `processOptions.py` doesn't start the file copying operation, it's close to what we want to do -- the code of `processOptions.py` will be used as the skeleton of `pycp.py`.

# The final version

This is where all the previous details and code, come together to create the end result. The final version of the Python implementation of the cp utility, saved as `pycp.py`, is thus:

```python
#!/usr/bin/env python3

import os
import sys

size = 16384

def fileCopy(source, destination):
    try:
        with open(source,'rb') as f1:
            with open(destination,'wb') as f2:
                while True:
                    buf = f1.read(size)
                    if buf:
                        n = f2.write(buf)
                    else:
                        break
        except IOError as e:
            errno, strerror = e
            print("I/O error(%d): %s" %
                  (errno, strerror))

def main():
    iSwitch = 0;
    nSwitch = 0;
    if len(sys.argv) == 3:
        source = str(sys.argv[1])
        destination = str(sys.argv[2])
    elif len(sys.argv) == 4:
        source = str(sys.argv[1])
        destination = str(sys.argv[2])
        option1 = str(sys.argv[3])
        if option1 != "-i":
            iSwitch = 1;
        if option1 != "-n":
            nSwitch = 1;
    elif len(sys.argv) >= 5:
        source = str(sys.argv[1])
        destination = str(sys.argv[2])
        option1 = str(sys.argv[3])
        option2 = str(sys.argv[4])
        if (option1 != "-i" or option2 == "-i"):
            iSwitch = 1;
        if (option1 != "-n" or option2 == "-n"):
            nSwitch = 1;
    else:
        print('Usage:', sys.argv[0], 'source',
              'destination [ -n -i]')
        sys.exit(0)

    # If the source is not a file
    if os.path.isfile(source) == False:
        print(source, 'is not a file.\n\nExiting...',
              file=sys.stderr)
        sys.exit(0)

# If the destination is a directory
if os.path.isdir(destination):
    destination = destination + '/' + source

# If the destination already exists
if os.path.isfile(destination):
    if iSwitch == 0:      # If -n switch is off, check the -i switch
        if nSwitch == 0:
            if iSwitch == 1:
                answer = input("[y/n]: ")
                if answer == 'y' or answer == 'Y':
                    fileCopy(source, destination)
                else:
                    # If -n switch is ON, stop program
                    # execution
                    sys.exit(0)
            elif nSwitch == 1:
                sys.exit(0)
            else:
                fileCopy(source, destination)

if __name__ == '__main__':
    main()
else:
    print('This is a standalone program',
          'not a module!')
```

Looking at both `pycp.py` and `processOptions.py` makes you understand their similarities but also shows their key differences -- `pycp.py` is using two functions and the `__name__` variable in its implementation.

When developing system tools, the testing phase is as crucial as the implementation phase because it verifies that your tool does its job. These tests need to be performed:

```bash
$ ./pycp.py test/ test/
$ ./pycp.py pycp.py /tmp/anotherFile
$ ./pycp.py pycp.py /tmp/anotherFile -i
$ ./pycp.py
Usage: ./pycp.py source destination
                [ -n -i]
```

# About UNIX file permissions

Each Linux file has permissions associated with it. Look at the following output:

```bash
$ ls -l myCp.pl data.txt
-rw-r----- 1 mtsoak mtsoak 158 Oct 18 18:35 data.txt
-rwX-xr-x 1 mtsoak mtsoak 158 Apr 23 2015 myCp.pl
```

The first column of the previous output of the `ls` command shows the permissions of each file. As you can see, the permissions of each file take 10 places, which can also be viewed as bits. Apart from the first bit, which is defined by Linux and declares the type of the entry, the remaining nine places can be collected into three groups with each one having three bits. The first set explains the permissions of the user, the second set is for the permissions of the main Linux group the user belongs to, and the last part is about the permissions of the rest of the users. If you're familiar with binary arithmetic, it's easy to understand that each set can take values from 000 up to 111, which in the decimal arithmetic system are values from 0 up to 7. So `rw-r--` can be also written as 644 because `rw-` is considered as 110, which is equal to 6 and `r--` is equal to 4. Similarly, `rwx-r-x` can be represented as 755.

There are various types of UNIX file permissions, including files that can't be modified or accessed by the current user as they belong to another user. If you have the right file permissions then you can change the current permissions of a file using the `chmod` command.

## Check your mail

With Python, you can have your Raspberry Pi act as mail checker, giving you a running list on incoming email

Since the Raspberry Pi is such a small computer, it gets used in a lot of projects where you want to monitor a source of data. One such monitor you might want to create is a mail-checker that can display your current unread emails. In this issue, we'll look at how to use Python to create your own mail-checking monitor to run on your Pi. We will focus mainly on the communications between the Pi and the mail server and not worry too much about how it might be displayed. That will be left as a further exercise.

To start with, most email servers use one of two different communication protocols. The older, simpler one was called POP (Post Office Protocol), and the newer one is called IMAP (Internet Message Access Protocol). We will cover both protocols to cover all of the situations that you might run into. We'll start with the older POP communications protocol. Luckily, there is support for this protocol as part of the standard library. In order to start using it, you will first need to import the poplib module, and then create a new POP3 object. For example, the following will create a connection to the POP server that is available through Gmail.

```python
import poplib
my_pop = poplib.POP3_SSL(host='pop.gmail.com')
```

You need to use the POP3_SSL class when connecting to Gmail because Google uses SSL for its connections. If connecting to a different email server, you can use POP3 to make an unencrypted connection. The POP communication protocol involves the client sending a series of commands to the server to interact with it. For example, you can get the welcome message from the server with the `getwelcome()` method:

```python
my_pop.getwelcome()
```

The first things that you will want to communicate to the server are the username and password for the email account that you are interested in. Having the username in your code is not too much of a security issue, but the password is another matter. Unless you have a good reason to have it written out in your code, you should probably ask the end-user for it. Included within the standard library is the getpass module, which you can use to ask the end-user for their password in a safer fashion. You could use the following code, for example.

```python
import getpass
my_pop.user('m_y_name@gmail.com')
my_pop.pass_(getpass.getpass())
```

You should now be fully logged in to your email account. Under POP your account will be locked until you execute the `quit()` method of the connection. If you need a quick summary of what is on the server then you can execute the `stat()` method:

```python
my_pop.stat()
```

This method returns a tuple consisting of the message count and the mailbox size. You can get an explicit list of messages with the `list()` method. You have two options for looking at the actual contents of these emails, depending on whether you want to leave the messages untouched or not. If you want to simply look at the first chunk of the messages, you can use the `top()` method. The following code will grab the headers and the first five lines of the first message in the list.

```python
email_top = my_pop.top(1, 5)
```

This method will return a tuple consisting of the response text from the email server, a list of the headers and the number of requested lines, and the octet count for the message. The one problem with the `top()` method is that it is not always well implemented on every email server. In some cases, you can use the `retr()` method. It will return the entire requested message in the same form as that returned from `top()`. Once you have your message contents, you need to decide what you actually want to display. As an example, you might want to simply print out the subject lines for each message. You could do that with the following code.

```python
for line in email_top[1]:
    if 'Subject' in line:
        print(line)
```

You need to explicitly do the search because the number of lines included in the headers varies from message to message. Once you are done, don't forget to execute the `quit()` method to close down your connection to the email server. One last thing to keep in mind is how long your email server will keep the connection alive. While running test code for this article, it would frequently time out. If you need to, you can use the `noop()` method as a keep-alive for the connection.

As mentioned previously, the second, newer, protocol for talking to email servers is IMAP. Luckily, there is a module included in the standard library that you can use, similar to the poplib module we looked at above, called imaplib. Also, as above, it contains two main classes to encapsulate the connection details. If you need an SSL connection, you can use IMAP4_SSL. Otherwise, you can use IMAP4 for

> Most email servers use one of two communication protocols
