# VARIABLE MANAGEMENT IN SHELL PROGRAMS 413

$$(var*pattern)
pares the beginning of the variable contents with the specified pattern. If the pattern is recognized, the construction returns the contents of the variable minus the shortest possible text that matches the search pattern. If the pattern is not found, the entire contents of the variable are returned. In the search pattern, the wildcards can be used for construction of file names (* ? [abc]). In no case is the variable changed:

```
user$ dat=/home/mk/book/book.tar.gz
user$ echo ${$(dat*/)}
home/mk/book/book.tar.gz
user$ echo ${$(dat.*)}
tar.gz
```

$$(var#pattern)
asas above, except that now the longest possible character string that matches the pattern is eliminated:

```
user$ dat=/home/mk/book/book.tar.gz
user$ echo ${$(dat##*/)}
book.tar.gz
user$ echo ${$(dat##.*)}
gz
```

$$(varXpattern)
as above, except that the pattern matching now takes place at the end of the variable. The shortest possible character string is eliminated from the end of the variable. The variable itself remains unchanged:

```
user$ dat=/home/mk/book/book.tar.gz
user$ echo ${$(dat**/)}
/home/mk/book
user$ echo ${$(datX.*)}
/home/mk/book/book.tar
```

$$(var##pattern)
as above, except that the longest possible character string is eliminated:

```
user$ dat=/home/mk/book/book.tar.gz
user$ echo ${$(dat##*/)}

-- no output --
user$ echo ${$(dat##.*)}
/home/mk/book
```

> On page 421 you will find an example which makes extensive use of the substitution commands introduced above for the purpose of copying or renaming groups of files (regmv *.ps *.eps).