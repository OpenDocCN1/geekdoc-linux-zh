```
for i; do
if [[ -r "$i" ]]; then
  max_word=
  max_len=
  for j in $(strings "$i"); do
    len=$#j
    if (( $len > max_len )); then
      max_len=$len
      max_word=$j
    fi
  done
  print "$i: '$max_word' ($max_len characters)"
fi
done
```

It runs scripts same way that bash does. This is expected, as zsh is intended to be a drop-in replacement for bash in most cases. A couple of things to note however.
First, zsh pipelines like the Korn shell does; the last command in a pipeline is executed in the current shell. Second, in zsh, the first element of an array is index 1, not 0 as it in bash and zsh.

Where zsh differs significantly is in the number of bells and whistles it provides for interactive use (some of which can be applied to scripting as well). Let's take a look at few:

# Tab Completion

Many kinds of tab completion are supported by zsh. These include command names, command options, and arguments.

When using the cd command, repeatedly pressing the tab key first displays a list of the available directories, then begins to cycle through them. For example:

```
me@linux ~ $ cd <tab>
```

```
me@linux ~ $ cd <tab>
Documents/ Downloads/ Music/ Pictures/ Public/
Desktop/ Videos/
me@linux ~ $ cd Desktop/<tab>
Documents/ Downloads/ Music/ Pictures/ Public/
Templates/ Videos/
me@linux ~ $ cd Documents/
Documents/ Downloads/ Music/ Pictures/ Public/
Templates/ Videos/
```

zsh can be configured to display a highlighted selector on the list of directories, and one can use the arrow keys to directly highlight the entry in the list to select it.

We can also switch directories by replacing one part of a path name with another:

```
me@linux ~ $ cd /usr/local/share
```

# 148 Other Shells