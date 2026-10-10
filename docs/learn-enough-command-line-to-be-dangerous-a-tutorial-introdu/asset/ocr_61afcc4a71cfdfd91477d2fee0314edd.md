![](bbox=[0.195, 0.145, 0.83, 0.385])

Figure 18: The correspondence between folders & directories.

```
$ /usr/local/bin
```

As seen in Figure 18, these representations correspond to directories in a hierarchical filesystem, with (say) **mhartl** a subdirectory of *User* and **ruby** a subdirectory of **mhartl**.

Conventions vary when speaking about directories: a *user directory* like /Users/mhartl would probably be read as “slash users slash mhartl” or “slash users mhartl”, whereas omitting the initial slash in spoken language is common for *system directories* such as /usr/local/bin, which would probably be pronounced “user local bin”. Because all Unix directories are ultimately subdirectories of the *root directory* / (pronounced “slash”), the leading and separator slashes are implied. **Note:** Referring to forward slashes incorrectly as “backslashes” is a *cause of suffering*, and should be strictly avoided.

The most important directory for a particular user is the *home directory*, which on my OS X system is /Users/mhartl, corresponding to my username (**mhartl**). The home directory can be specified as an *absolute path*, as in /Users/mhartl, or using the shorthand for the home directory is the

61