# USER LOGIN 133

connections and the selected speeds. The individual lines have the following
format:

speed #init-flags #final-flags #login-string #next-speed

After each entry, an empty line must be inserted; the first line is the default
setting if no speed is specified at the call of the getty. Comments are marked by a #
at the beginning of a line. When changes have been made to this file, the
command getty -c should be used to check the syntax of this file because
the event of syntax errors in this file, no login to the system will be possible.
speed is the symbolic specification of the speed specified as a parameter
the call of getty. If the same value is entered for next-speed, the speed
cannot be changed. Otherwise, the Break key can be used to toggle between the
different speeds.

The init-flags and final-flags values determine the initial and
final TERMIO settings. Usually, no modification is needed. For my
terminal, the XON/XOFF protocol had to be switched off; thus I included
the additional settings -IXON -IXOFF in the final-flags. The flags to
specified here are exactly the same parameters as the ones known to the stty
program. Interested users should refer to the main page for stty(1).

login-string contains the text displayed as the login prompt. As with
the output of the /etc/issue file, a series of special character sequences is
substituted. Table 4.10 shows a list of these character sequences and their
substitutions.