satisfied with the changes, you wrote the altered buffer out to the file and end the session.

A window's Mode Line has an indicator immediately to the left of emacs: that shows the modification state of the buffer in the window. Its three states are -- (not modified), ** (modified), and %% (readonly).

The emacs editor keeps a record of all the keys you have pressed (text and commands) since the beginning of the editing session, up to a limit currently set at 20,000 characters. If you are within the limit, it is possible to undo the entire session for this buffer, one change at a time. If you have multiple buffers (page 500), each buffer has its own record.

Undo is considered so important that it is given a backup-key sequence, in case some keyboards cannot easily handle the primary sequence. The two sequences are CONTROL-u (underscore, which on OSR-33 TTY keyboards is LEFT-CONTROL-x). When you type CONTROL-, emacs undo the command and moves the cursor to that position in the buffer, so you can see what happened. If you type CONTROL-, a second time, the next to the last is undone, and so on. If you keep on typing CONTROL-, eventually you get the buffer back to its original modified state, and the ** Mode Line indicator changes to -- This is in contrast to the original vi, where undo works only on the most recent commands.

When you break the string of Undo commands with anything (text or any command except Undo), all the reverse changes you made during the string of undo become a part or all the change record and can themselves be undone. This offers a way to redo some or all the undos. If you decide you backed too far, type a command (something innocuous, such as CONTROL-f that does not change the buffer), and begin undoing in reverse. Table 11-5 lists some examples.

# Commands

| | table 11-5 |
|---|---|
| CONTROL- | Undoes the last change |
| CONTROL-F CONTROL- | Undoes the last change and changes it back again |
| CONTROL-- | Undoes the last two changes |
| CONTROL--CONTROL-F CONTROL-- | Undoes two changes and changes both back again |
| CONTROL--CONTROL-F-CONTROL- | Undoes two changes and changes one of them back again