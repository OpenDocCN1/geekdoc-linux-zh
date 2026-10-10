# Table 7.1 Typical Linux/UNIX Shell Programs

| NAME | DESCRIPTION |
|---|---|
| ash | A Bourne shell clone that supports all Bourne shell commands but is smaller than Bash. |
| ash.static | A version of ash that is not dependent on software libraries. |
| bash | Stands for Bourne Again Shell, the default Linux shell. An sh-compatible interpreter, it reads standard input or input from a file; incorporates features from both Korn and C shells; and is intended to conform with IEEE POSIX Shell and Tools Specifications. |
| mc | Midnight Commander, a visual shell. It looks like a file manager but has many more features. |
| pdksh | A reimplementation of the Korn shell intended for interactive and shell script use. |
| rsh | The restricted shell used for network operations. |
| sash | A statically linked shell that contains simplified versions of some basic commands. It is useful for system recovery. |
| tcs h | An enhanced version of the C shell with additional features and fancier prompts. In Linux, this shell is the usual choice as the alternative to Bash. |
| zsh | An enhanced version of the Bourne shell with most Korn shell, Bash, and tcsh features (and more). |

variable value. Although Bash is the usual default shell, you can specify which shell you want to use—either by default or for a specific process or task. On some systems, you can change your shell with commands such as chsh or passwd with the -s option. For further help, check your information sources.

# Example 7.1 Which Is the Login Shell?

Freston, an experienced shell programmer, is contemplating changing his login shell. But first, he would like to see what shell he logs into by default. He types

```
# cat /etc/passwd⏎
```

Freston's one-line password profile,