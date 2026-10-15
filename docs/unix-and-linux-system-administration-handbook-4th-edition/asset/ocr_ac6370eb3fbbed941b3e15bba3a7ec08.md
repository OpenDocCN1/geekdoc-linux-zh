split would run in "scalar context" and return only the number of fields that it found. Functions you write can distinguish between scalar and list contexts, too, by using the wantarray function. It returns a true value in list context, a false value in scalar context, and an undefined value in void context.

The line

```
%uids_by_name = reverse %names_by_uid;
```

has some hidden depths, too. A hash in list context (here, as an argument to the reverse function) evaluates to a list of the form (key1, value1, key2, value2,...). The reverse function reverses the order of the list, yielding (valueN, keyN, ..., value1, key1). Finally, the assignment to the hash variable %uids_by_name converts this list as if it were (key1, value1, ...), thereby producing a permuted index.

# References and autovivification

These are advanced topics, but we'd be remiss if we didn't at least mention them. Here's the executive summary. Arrays and hashes can only hold scalar values, but you will often want to store other arrays and hashes within them. For example, returning to our previous example of parsing the /etc/passwd file, you might want to store all the fields of each passwd line in a hash indexed by UID.

You can't store arrays and hashes, but you can store references (that is, pointers) to arrays and hashes, which are themselves scalars. To create a reference to an array or hash, you precede the variable name with a backslash (e.g., @array) or use reference-to-array or reference-to-hash literal syntax. For example, our passwd-parsing loop would become something like this:

```
while (<>) {
  $array_ref = [ split /:/ ];
  $passwd_by_uid[$array_ref->[2]] = $array_ref;
}
```

The square brackets return a reference to an array containing the results of the split. The notation $array_ref->[2] refers to the UID field, the third member of the array referenced by $array_ref.

$array_ref[2] won't work here because we haven't defined an @array_ref array; $array_ref and @array_ref are different variables. Furthermore, you won't receive an error message if you mistakenly use $array_ref[2] here because @array_ref is a perfectly legitimate name for an array; you just haven't assigned it any values.

This lack of warnings may seem like a problem, but it's arguably one of Perl's nicest features, a feature known as "autovivification." Because variable names and referencing syntax always make clear the structure of the data you are trying to access, you need never create any intermediate data structures by hand. Simply make an assignment at the lowest possible level, and the intervening structures materialize automatically. For example, you can create a hash of references to arrays whose contents are references to hashes with a single assignment.