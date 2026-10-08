```
TRUE=1
if [ "$TRUE" ] ; # if true and if : also work.
then
  read name
  echo $name
  fi "$Filename"
fi
#
# Reads only first line of file.
# An "if/then test has no way of iterating unless embedded in a loop.
exit 0
```

# Example 20-11. Data file names for above examples

+   - Aristotle
- Arrhenius
- Belisarius
- Capablanca
- Dickens
- Euler
- Goethe
- Hegel
- Jonah
- Laplace
- Maroczy
- Purcell
- Schmidt
- Schopenhauer
- Semmelweiss
- Smith
- Steinmetz
- Tukhashevsky
- Turing
- Venn
- Warzawski
- Znosko-Borowski

# This is a data file for
#+ "redir2.sh", "redir3.sh", "redir4.sh", "redir4a.sh", "redir5.sh".
Redirecting the stdout of a code block has the effect of saving its output to a file. See Example 3-2.

Here documents are a special case of redirected code blocks. That being, it should be possible to feed the output of the header into the stdin for a while loop.

# This example by Albert Siersma
# Used with permission (thanks!)

```
function doesOutput() {
  # Could be an external command too, of course.
  # Here we show you can use a function as well.

  ls -al .jpg | awk '{print $5,$9}'
}
```

nr=0 # We want the loop to be able to manipulate these and
totalSize=0 # to be able to see the changes after the 'while' finished.

# Chapter 20. I/O Redirection