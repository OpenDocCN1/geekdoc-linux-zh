```
/usr/share/zsh/4.2.5/functions/Completion/Base
/usr/share/zsh/4.2.5/functions/Completion/Cygwin
/usr/share/zsh/4.2.5/functions/Completion/Darwin
/usr/share/zsh/4.2.5/functions/Completion/Debian
/usr/share/zsh/4.2.5/functions/Completion/Linux
/usr/share/zsh/4.2.5/functions/Completion/Mandrake
/usr/share/zsh/4.2.5/functions/Completion/Redhat
/usr/share/zsh/4.2.5/functions/Completion/Unix
/usr/share/zsh/4.2.5/functions/Completion/X
/usr/share/zsh/4.2.5/functions/Completion/MIME
/usr/share/zsh/4.2.5/functions/Prompts
/usr/share/zsh/4.2.5/functions/TCP
/usr/share/zsh/4.2.5/functions/Zftp
/usr/share/zsh/4.2.5/functions/Zle
%
```

As you can see, there are lots of places where the zsh shell goes hunting to resolve function names. On my system, I can place my functions in the /usr/local/share/zsh/site-functions directory, and the zsh shell will be able to resolve them.

However, before the zsh shell can resolve the function, you must use the autoload command. This command loads the function into memory for the shell to access.

Here's an example of a stand-alone function:

```
% cat dbl
#!/bin/zsh
# a function to double a value
dbl() {
  value=$(( $1 * 2 )
  return $value
}
% cp dbl /usr/local/share/zsh/site-functions
%
```

Okay, the function is created in a file and stored in a directory in the fpath. If I try to use it though, I'll get an error message until I load it into memory:

```
% dbl 5
zsh: command not found: dbl
% autoload dbl
% dbl 5
% echo $?
10
%
```