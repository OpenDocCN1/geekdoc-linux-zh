Once the user enters the recipient's e-mail address and presses the Enter/Return key on his or her keyboard, the trailing newline is actually captured as part of the input. We use the chomp function to cleanly remove this end of line character from the input, as stored in the $email variable. If we don't remove it, we would have a difficult time determining if the user entered an address, since $email will still evaluate to true because it would have a length of atleast one - from the newline character.

# **Checking E-Mail Address**

Next, we check to see if $email is false, which would occur if the user did not enter an address, and if so, we simply execute the loop again. This provides the user another chance to enter the address. However, if an address was entered, we ask the user for confirmation and exit from the loop. An advanced application might also check the validity of the e-mail address, but we are not doing it here. If you are interested in adding such functionality, you should install the Email::Valid module, as shown in the *Installing Extensions* section, and then change this application in the following manner:

```
```
#!/usr/bin/perl
    use Mail::Send;                    ## Import/use Mail::Send
    use Email::Valid;                  ## Import/use Email::Valid
    use strict;                        ## Enable "strict" pragma
    ...
    while (1) {
        ...
        next if (! $email);                    ## Repeat loop if no $email

        if (!Email::Valid->address ($email)) {
            ## E-Mail address is not valid
            print "The e-mail address you entered is not in a valid format.\n";
        }
        ...
    }
    ...
    exit (0);
```
```

We use the address function, defined in the Email::Valid module, to check whether the specified e-mail address conforms to the RFC 822 specification, Standard for the Format of ARPA Internet Text Messages. The function simply checks the syntax; there is no way to determine whether a specific address is deliverable without actually attempting delivery.