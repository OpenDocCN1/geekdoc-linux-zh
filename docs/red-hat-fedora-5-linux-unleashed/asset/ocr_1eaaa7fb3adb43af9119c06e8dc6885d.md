Named for Randal Schwartz, a *Schwartzian transform* is a way of sorting an array by something that is not obvious. The sort function sorts arrays alphabetically, that is pretty obvious. What if you want to sort an array of strings alphabetically by the third word? Perhaps you want something more useful, such as sorting a list of files by file size? A Schwartzian transform creates a new list that contains the information that you want to sort by, referencing the first list. You then sort the new list and use it to figure out the order that the first list should be in. Here’s a simple example that sorts a list of strings by length:

```
```
@sorted_by_length =
    map { $_->[0] }        # Extract original list
    sort { $a->[1] <=> $b->[1] }  # Sort by the transformed value
    map { [$_, length($_)] }      # Map to a list of element lengths
    @list;
```
```

Because each operator acts on the thing immediately to the right of it, it helps to read this from right to left (or bottom to top, the way it is written here).

The first thing that acts on the list is the **map** operator. It transforms the list into a hash in which the keys are the list elements and the values are the lengths of each element. This is where you put in your code that does the transformation by which you want to sort.

The next operator is the **sort** function, which sorts the list by the values. Finally, the hash is transformed back into an array by extracting its keys. The array is now in the desired order.

# Command-Line Processing

Perl is great at parsing the output of various programs. This is a task for which many people use tools such as awk and sed. Perl gives you a larger vocabulary for performing these tasks. The following example is very simple, but illustrates how you might use Perl to chop up some output and do something with it. In the example, Perl is used to list only those files that are larger than 10KB:

```
```
$ ls -la | perl -nae 'print "${f[0]} is ${f[4]}\n"  if ${f[4]} > 10000;'
```
```

The -n switch indicates that I want the Perl code run for each line of the output. The -a switch automatically splits the output into the @F array. The -e switch indicates that the Perl code is going to follow on the command line.