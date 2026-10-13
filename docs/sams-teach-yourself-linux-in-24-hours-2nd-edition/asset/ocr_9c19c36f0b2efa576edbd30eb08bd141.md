# Entering Appointments

After you restart emacs, you can enter appointment reminders in your diary with the emacs appt-add command. First, enter the calendar mode, and click your left mouse button on a specific day. Next, press and release the Escape key, type an x, then type appt-add, and press Enter. You're asked, at the command line at the bottom of the emacs window, for an appointment time in hours and minutes, like so:

```
Time (hh:mm[am/pm]):
```

Enter the time in the form of a 24-hour clock (such as 15:00) or a 12-hour clock (such as 3:00 pm). After you press Enter, you're prompted for a message, like so:

```
Message:
```

Type in a reminder message (such as "Wake up!"), and press Enter again.

Five minutes before the appointment time, emacs beeps and then displays a new mode line, informing you of the appointment. Two minutes later, the same thing happens. You can also manually add reminders to your diary file, for example:

+   8:00am Jogging with dog
+   12:00am Lunch with Cathy
+   15:00pm Check with car repair shop

You can save these reminders following each date in your diary files to set future appointments. If you want to delete appointments, use the appt-delete command after selecting a specific day. You're asked interactively to delete various appointments from your diary.

By using the emacs calendar mode and appointment functions, you can build a history of your appointments in your personal diary. Experiment with different modes, and read the emacs info files for more information.

# Setting Alarms with the knotes Client

You don't need to run large programs or word processors in order to set alarms when you use the K Desktop Environment, or KDE. If you want to try an easy-to-use utility to set reminders or alarms during your X sessions, try the knotes client, included with the KDE utilities distribution.

Click the Utilities menu on your KDE desktop's panel and select knotes. A small Post-It™-like window will appear on your desktop. Type in some text, and then right-click in the knotes window. From the pop-up menu, scroll down, select the Operations menu, and then click the Alarm menu item, as shown in Figure 18.5.