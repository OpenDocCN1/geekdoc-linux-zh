In general, when looking for some action to turn into a procedure, see what actions tend to happen a lot in a log. Most programs spend a lot of time displaying things to the screen. Such procedures as Write Writelin become general-purpose tools that may be used all over your programs. Furthermore, once you've written and tested them, they may be reused in future programs as well without adding to the burden of code that you must test for bugs.

Try to look ahead to your future programming tasks and create procedures of general usefulness. I show you more of those by way of examples as we continue, and tool building is is a very good way to hone your assembly language skills.

On the other hand, a short sequence (5 to 10 instructions) that is only called once or perhaps twice within a middling program (that is, over hundreds of machine instructions) is a poor candidate for a procedure.

You may find it to define large procedures that are called only once when your program becomes big enough to require breaking it down into functional chunks. A thousand-line assembly language program might split well into a sequence of 9 or 10 larg procedures. Each is only called once from the main program, but this allows your main program to be very indicative of what the program is doing:

```
Start: call Initialize
call OpenFile
Input: call GetRec
call VerifyRec
call WriteRec
loop Input
call CloseFile
call CleanUp
call ReturnTodos
```

This is clear and readable and provides a necessary view from a height when you begin to approach a thousand-line assembly language program. Remember that the Martians are always hiding close by, anxious to turn your program into unreadable hieroglyphics.

There's no weapon against them with half the power of procedures.

# Using BIOS Services

In the last chapter we looked closely at DOS services, which are accessed through the DOS services dispatcher. The DOS dispatcher lives at the