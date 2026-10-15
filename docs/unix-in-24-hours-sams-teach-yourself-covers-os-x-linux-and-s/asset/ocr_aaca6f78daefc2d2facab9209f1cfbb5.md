```
case $filename in
  *.gif(*.jpg )
    echo "<li><img src=$directory/$filename><br />"
    showname $filename
    ;;
  *.html(*.html )
    echo "<li><a href=$filename>$filename</a></li>" ;;
  *)
    if [ -d $filename ] ; then
      echo \
      "<li><tt><a href=$iamcalled?$directory/$filename>"
      echo "[$filename]</a></tt></li>"
    else
      echo "<li>"
      showname $filename
    fi
    ;;
esac
done
}
```

It’s now easy to add error checking in the function (the -d test to see whether it’s a directory before moving there with the cd command).

Functions can be quite complex, but even simple functions can help you get the most out of your shell interaction.

# Summary

In this hour, you’ve just skimmed the basics of shell programming. You were introduced to the control structures of the shell and to two important commands. You can learn much more about shell programming; my popular book Wicked Cool Shell Scripts (No Starch Press, 2015) is one place you can dig much deeper into the subject.

# Workshop

The Workshop summarizes the key terms you’ve learned and poses some questions about the topics presented in this lesson. It also provides you with a preview of what you will learn in the next hour.

# Key Terms

command block A list of one or more shell commands can be grouped in a conditional or looping statement, called a command block.

conditional expression This is an expression that returns either true or false.

determinate loop In this type of loop, the number of times the loop is run is known before the loop is started.

expression This is a command that returns a value.

indeterminate loop In this type of loop, the number of times the loop is run is not known before the loop is started.

loop This is a sequence of commands that are repeatedly executed while a condition is true.