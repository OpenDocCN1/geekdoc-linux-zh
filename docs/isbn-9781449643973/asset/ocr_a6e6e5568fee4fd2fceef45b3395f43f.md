28. Password: ISS316Security

29. Navigate to the `/archive/2001` directory. Type the command: `cd /archives/2001` and press `<enter>`.

30. Perform a directory listing and notice the permissions of `financials.txt`. Type the command: `ls -ls financials.txt` and press `<enter>`. Notice the student user & student group has read and write permissions at the file level.

31. Open `financials.txt` for edit in vim editor: Type the Command `vi financials.txt` and press `<enter>`.

32. Press the "i" key to enter INSERT mode.

![](bbox=[0.18, 0.32, 0.84, 0.74])

**Figure 22 – Attempting to edit a file on a Read Only filesystem**

33. View the notice “Warning: Changing a readonly file”.

34. Press the *escape* key to exit from insert mode, then press the “shift” & “:” keys to enter command mode. At the colon prompt in command mode, type `q` to exit.