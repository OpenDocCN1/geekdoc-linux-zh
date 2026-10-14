```
max_len=$len
max_word=$j
fi
done
echo "$i: '$max_word' ($max_len characters)"
fi
shift
done
```

Next, we will compare the efficiency of the two versions by using the time command:

```
[me@linuxbox ~]$ time longest-word2 dirlist-usr-bin.txt
dirlist-usr-bin.txt: 'scrollkeeper-get-extended-content-list' (38 characters)

real    0m3.618s
user    0m1.544s
sys     0m1.768s
[me@linuxbox ~]$ time longest-word3 dirlist-usr-bin.txt
dirlist-usr-bin.txt: 'scrollkeeper-get-extended-content-list' (38 characters)

real    0m0.060s
user    0m0.056s
sys     0m0.008s
```

The original version of the script takes 3.618 seconds to scan the text file, while the new version, using parameter expansion, takes only 0.06 seconds—a very significant improvement.

# Arithmetic Evaluation And Expansion

We looked at arithmetic expansion in Chapter 8. It is used to perform various arithmetic operations on integers. Its basic form is:

```
$((expression))
```

where expression is a valid arithmetic expression.

This is related to the compound command (( )) used for arithmetic evaluation (truth tests) we encountered in Chapter 28.

In previous chapters, we saw some of the common types of expressions and operators. Here, we will look at a more complete list.