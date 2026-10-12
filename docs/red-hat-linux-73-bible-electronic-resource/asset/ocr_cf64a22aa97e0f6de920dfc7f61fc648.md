+   • **Automatically mount CD when inserted** — If this is selected, when a data CD is inserted it is automatically mounted in a subdirectory of /mnt. This option is on by default.

+   • **Automatically start auto-run program on newly mounted CD** — If this is selected, after a data CD is mounted, the user is asked to choose whether to run an auto-run program from the CD. This option is on by default if the first option is checked.

+   • **Open file manager window for newly mounted CD** — If this is selected, after a data CD is mounted, a file manager window opens to display the contents of the top-level directory of the CD. For the first CD drive, the directory is /mnt/cdrom. This option is on by default if the first option is checked.

+   4. For Audio CDs, you can select Run Command When CD Is Inserted to have the CD start playing automatically after it's inserted. The command shown in the box labeled Command is used to play the CD. By default, the option is on, and the `gtcd` command is used, though you can change the CD player to any player you prefer.

+   5. Click **OK**.

# ### Playing CDs with gtcd

The `gtcd` CD player is the one that pops up automatically when you insert a CD as you use the Gnome desktop. This player has controls that look similar to what you would see on a physical CD player. If you are using the Gnome desktop, from the System Menu select Programs → Multimedia → CD Player; from a Terminal window, type

```
$ gtcd &
```

# #### Adding track information

The interface for adding information about the CD and its tracks is very nice. Click the Open Track Editor button. If you have an active connection to the Internet, `gtcd` automatically tries to grab track information for your CD. So, you may already see the CD title and track name for each song when you open the editor.

If information about the CD doesn't appear, you can add Artist and Title information about the CD yourself. Then you can select each track to type in the track name. To add the name of the artist and the CD name, click in the Artist/Title box and type in that information. Figure 8-2 shows the CD Player and the Track Editor.