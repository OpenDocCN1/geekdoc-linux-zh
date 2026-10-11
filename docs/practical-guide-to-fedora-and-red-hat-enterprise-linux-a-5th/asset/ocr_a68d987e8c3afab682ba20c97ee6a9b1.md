![](bbox=[0.35, 0.1, 0.83, 0.35])

Figure 4-28 The screen displayed by info coreutils after you type /sleepRETURN twice

After giving the command info coreutils, press the SPACE bar a few times to scroll through the display. Type /sleepRETURN to search for the string sleep. When you type /, the cursor moves to the bottom line of the window and displays Search for string [string], where string is the last string you searched for. Press RETURN to search for string or enter the string you want to search for. Typing sleep displays sleep on that line, and pressing RETURN displays the next occurrence of sleep.

Now type /RETURN (or /sleepRETURN) to search for the next occurrence of sleep as shown in Figure 4-28. The asterisk at the left end of the line indicates that this entry is a menu item. Following the asterisk is the name of the menu item and a description of the item.

Each menu item is a link to the info page that describes the item. To jump to that page, search for or use the ARROW keys to move the cursor to the line containing the menu item and press RETURN. With the cursor positioned as it is in Figure 4-28, press RETURN to display information on sleep. Alternatively, you can type the name of the menu item in a menu command to view the information: To display information on sleep, for example, you can give the command m sleep, followed by RETURN (When you type m (for menu), the cursor moves to the bottom line of the window as it did when you typed /) and displays Menu item:. Typing sleep displays sleep on that line, and pressing RETURN displays information about the menu item you have chosen.

Figure 4-29 (on the next page) shows the top node of information on sleep. A node groups a set of information you can scroll through with the SPACE bar. To display the next node, press p to display the previous node.

As you read through this book and learn about new utilities, you can use man or info to find out more about those utilities. You can print PostScript documents, you can print a manual page by using the man utility with the -t option (for example, man -t cat | lp prints information about the cat utility). You can also use a Web browser to display the documentation at www.tldp.org, docs.fedoraproject.org, or www.redhat.com/docs and then print the desired information from the browser.