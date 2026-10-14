the completion is successful.

While this example shows completion of pathnames, which is its most common use, completion will also work on variables (if the beginning of the word is a $), usernames (if the word begins with ~), commands (if the word is the first word on the line), and hostnames (if the beginning of the word is @). Hostname completion works only for hostnames listed in /etc/hosts.

A number of control and meta key sequences are associated with completion, as listed in Table 8-4.

# Table 8-4: Completion Commands

| Key | Action |
|---|---|
| ALT-? | Display a list of possible completions. On most systems, you can also do this by pressing the TAB key a second time, which is much easier. |
| ALT-* | Insert all possible completions. This is useful when you want to use more than one possible match. |

There are quite a few more that are rather obscure. A list appears in the bash man page under “READLINE.”

# PROGRAMMABLE COMPLETION

Recent versions of bash have a facility called programmable completion. Programmable completion allows you (or more likely, your distribution provider) to add more completion rules. Usually this is done to add support for specific applications. For example, it is possible to add completions for the option list of a command or match particular file types that an application supports. Ubuntu has a fairly large set defined by default. Programmable completion is implemented by shell functions, a kind of mini shell script that we will cover in later chapters. If you are curious, try the following: