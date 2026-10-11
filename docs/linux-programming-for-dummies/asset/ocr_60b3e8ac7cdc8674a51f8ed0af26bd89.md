# Chapter 8

# The case Statement

In This Chapter

+   ➤ Using the case statement
+   ➤ Making the program follow at least one instruction
+   ➤ Putting the case statement in the user interface

You can run into a problem if you tell your computer to make a decision with many possibilities. Say, for example, that you want your computer to do something unique with each of five offices in your company. Your program requires a bunch of if / elif statements, as in the following example:

```
if [ $region =eq "1" ]
then
    echo "Hello, Bob"
    elif [ $region =eq "2" ]
    then
    echo "Hello, Mary"
    elif [ $region =eq "3" ]
    then
    echo "Hello, Joan"
    elif [ $region =eq "4" ]
    then
    echo "Hello, Mike"
    elif [ $region =eq "5" ]
    then
    echo "Hello, Tom"
fi
```

This program is probably a mess for you to read — although your computer can read it just fine. But just try to imagine tracking 20 if statements if you need to update 20 regional offices!

In this chapter, I show you how to make your program make decisions efficiently by using the case statement.