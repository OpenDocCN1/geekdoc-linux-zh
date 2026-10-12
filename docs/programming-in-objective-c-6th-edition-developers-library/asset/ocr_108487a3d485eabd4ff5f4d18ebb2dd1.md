```
E 2 28 2016
T
```

Program 8.4 Output (Rerun)

```
E 2 22 2015
T
```

Inside m      , the statement n illustrates the ability to pass a structure to a function and to return one as well. The d function has the appropriate declaration to indicate that the function returns a value of type ⌧ d . Inside the function is the same code that was included in the m routine of Program 8.3. The functions n and i remain unchanged from that program. Make certain that you understand the hierarchy of function calls in the preceding program: The m function calls d , which in turn calls n , which itself calls the function i .

# A Structure for Storing the Time

Suppose you have the need to store values inside a program that represents various times expressed as hours, minutes, and seconds. Because you have seen how useful our d structure has been in helping you to logically group the day, month, and year, it seems only natural to use a structure that you could call appropriately enough, t , to group the hours, minutes, and seconds. The structure definition is straightforward enough, as follows:

```
⌧
{

}
```

Most computer installations choose to express the time in terms of a 24-hour clock, known as military time. This representation avoids the hassle of having to qualify a time with a.m. or p.m. The hour begins with 0 at 12 midnight and increases by 1 until it reaches 23, which represents 11:00 p.m. So, for example, 4:30 means 4:30 a.m., whereas 16:30 represents 4:30 p.m.; and 12:00 represents noon, whereas 00:01 represents 1 minute after midnight.

Virtually all computers have a clock inside in the system that is always running. This clock is used for such diversified purposes as informing the user of the current time, causing certain events to occur or programs to be executed at specific times, or recording the time that a particular event occurs. One or more computer programs are usually associated with the clock. One of these programs might be executed every second, for example, to update the current time that is stored somewhere in the computer's memory.