# Wildcards and Regular Expressions

1. Begin by making sure you have a test file to work with. The example shows the testme file from the previous uniq examples:

```
% cat testme OWL/ keylime.pie
Archives/ bin/ src/
Infolist-d/ bitnet.mailing-lists.Z temp/
Mail/
News/ drop.test.hqx testme
```

2. The general form of grep is to specify the command, any flags you want to add, the pattern, and a line:

```
% grep bitnet_testme bitnet.mailing-lists.Z temp/
Mail/
```

As you can see, grep easily pulled out the line in the testme file that contained the pattern, bitnet.

3. Be aware that grep finds patterns in a case-sensitive manner:

```
% grep owl testme
%
```

Note that OWL was not found because the pattern specified with the grep command was all lowercase, owl.

But that's when the -i flag can be helpful, which causes grep to ignore case:

```
% grep -i owl testme
Archives/ OWL/ keylime.pie
```

4. For the next examples, I'll move into the /etc directory because some files there have lots of lines. The we shows that the file /etc/passwd has almost 4000 lines:

```
% cd /etc
% wc -l /etc/passwd
3887
```

My account is Taylor. I'll use grep to see my account in the password file:

```
% grep /etc/passwd
taylorj?:2048:1375:James Taylor:/users/taylor:/bin/csh
taylorj?:760:1375:James Taylor:/users/usr/local/bin/tcsh
taylord?:375:518:Dave Taylor:/users/taylor:/usr/local/lib/msh
taylorjr?:203:1022:James Taylor:/users/taylorjr:/bin/csh
taylorrj?:668:1042:Robert Taylor:/users/taylorrj:/bin/csh
taylorm?:862:1508:Melanie Taylor:/users/taylormx:/bin/csh
taylorj?:1989:1412:Dave Taylor:/users/taylor:/bin/csh
```

Try this on your system, too.