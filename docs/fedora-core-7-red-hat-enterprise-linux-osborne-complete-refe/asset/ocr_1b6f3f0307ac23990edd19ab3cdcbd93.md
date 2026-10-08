event on your command line. Pressing it again places the next history event on your command. Pressing the DOWN ARROW key places the previous event on the command line.

You can use certain control and meta keys to perform other history operations like searching the history list. A meta key is the ALT key, and the ESC key on keyboards that have no ALT key. The ALT key is used here. ALT-< will move you to the beginning of the history list; ALT-N will search it. CTRL-S and CTRL-R will perform incremental searches, display matching commands as you type in a search string. Table 8-4 lists the different commands for referencing the history list.

> *TIP* *If more than one history event matches what you have entered, you will hear a beep, and you can then enter more characters to help uniquely identify the event.*

You can also reference and execute history events using the ! history command. The ! is followed by a reference that identifies the command. The reference can be either the number

| History Commands | Description |
|---|---|
| CTRL-N OR DOWN ARROW | Moves down to the next event in the history list |
| CTRL-P OR UP ARROW | Moves up to the previous event in the history list |
| ALT-< | Moves to the beginning of the history event list |
| ALT-> | Moves to the end of the history event list |
| ALT-N | Forward Search, next matching item |
| ALT-P | Backward Search, previous matching item |
| CTRL-S | Forward Search History, forward incremental search |
| CTRL-R | Reverse Search History, reverse incremental search |
| fc event-reference | Edits an event with the standard editor and then executes it |
| Options | -1 List recent history events; same as **history** command |
| | -e editor event-reference Invokes a specified editor to edit a specific event |
| | |

| History Event References | Description |
|---|---|
| !event num | References an event with an event number |
| ! ! | References the previous command |
| !characters | References an event with beginning characters |
| !?pattern? | References an event with a pattern in the event |
| ! -event num | References an event with an offset from the first event |
| !num-num | References a range of events |
| | |

**TABLE 8-4** History Commands and History Event References