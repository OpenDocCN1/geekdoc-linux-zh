```
echo "u -- to save as uppercase"
echo "1 -- to save as lowercase"; }

case $1
in
p | -p)    print $@;;
u | -u)    upper $@;;
1 | -1)    lower $@;;
*)         usage_error $0;;
esac
```

# # Summary

This chapter introduced you to many of the features of the bash, posh, and tcsh pro- gramming languages. As you become familiar with using Linux, you will find that you use shell programming languages more and more often.

Even though the shell languages are very powerful and also quite easy to learn, you might run into some situations where shell programs are not suited to the problem you are solving. In these cases, you may want to investigate the possibility of using one of the other languages available under Linux. At this point, there are a lot of other pro- gramming languages you may want to look at. To learn more about:

awk, which is useful for handling both search patterns and large columns of num- bers, see Chapter 25, “gawk.”

Perl, useful for many quick script tasks as well as Web pages, see Chapter 28, “Perl.”

Smalltalk/X, which is used to program object-oriented applications under the X GUI, see Chapter 31, “Smalltalk/X.”

![](bbox=[0.84, 0.6, 0.98, 0.77])