
## Using the plan Client

Thomas Driemeyer's *plan* client, and associated appointment and scheduling daemon, *planD*, is a graphical calendar program and appointment scheduler for X. If you have the screen real estate, you can use *plan* without its scheduling daemon as a simple visual calendar. If, however, you want to take advantage of its scheduling and appointments, then you should start the daemon as requested when you first run *plan*.

This client requires an active X session. You can start *plan* from the command line of an X terminal window like this:

```
$ plan &
```

After you press Enter, you will see a small dialog box that asks if you want to start the daemon. If so, press the Start daemon now button, or press the Continue without daemon button to use *plan* as a simple calendar. The *plan* client appears as shown in Figure 12.4, with the current day highlighted in green.

To get started, select a desired day, month, or year, then click on a day. You will see a pop-up dialog box, as shown in Figure 12.5 that features entries for schedule and appointment information. When finished, click the Done button to save your appointment.

The *plan* client has extensive built-in and context-sensitive functions you can use to explore the program's features and to get help. You can also read its manual page for more information.

![](img/1ea833f5a3e3c1547e3dd2891f52804a_297_0.png)

**Figure 12.4** *The plan client has a corresponding plan daemon that is used to provide schedule and appointment alarms.*

![](img/1ea833f5a3e3c1547e3dd2891f52804a_298_0.png)

**Figure 12.5** *The plan client's scheduling dialog box has many different controls and settings you can use to handle appointments.*

## Using KDE's kalendar Client

The K Desktop Environment has a feature-rich assortment of productivity tools. There is not enough room in this chapter to explore all of them (i.e., *knotes*, which also features alarms, and *karm*, which is a personal time tracker). However, you will find Mark Redding’s *kalendar* client to be a comprehensive and capable calendar tool that features to-do lists, along with event and appointment tracking.

You can start *kalendar* from KDE’s desktop panel, or the command line of an X terminal window like this:

```
$ kalendar &
```

After you press Enter, you will see the main window, as shown in Figure 12.6.

![](img/1ea833f5a3e3c1547e3dd2891f52804a_298_1.png)

**Figure 12.6** *The KDE kalendar client is a graphical calendar with a host of information-tracking features.*

The default view is of a single day's entries. By using the **View** menu, you can switch this view to include a week, month, or entire year! Appointments are entered using the **Appointment** menu's **New** menu item. New events are also entered by using the **Event** menu's **New** menu item. You can search through your appointments, and use the graphic toolbar to delete appointments. Note that after you launch *kalendar*, a small floating window also appears on your desktop. You can use this window to minimize or maximize the main *kalendar* window.

This client also includes security features to limit access to appointment or calendar entries. To get help on using *kalendar*, select the **Help** menu on the far right of the menu bar, then click **Help**.

## X11 Organizers

This section introduces two sophisticated software program organizers you can use to maintain or increase your productivity while using Linux. These clients have features that go beyond simple calendar and appointment scheduling programs.

### Using korganizer

The KDE *korganizer* client is a scheduling and organizing application like *plan*, which includes a scheduling daemon that runs in the background during your X session. The *kalendar* client, like the *korganizer*, has an accompanying small window application that can be used to launch a new view of your schedule.

You can start *korganizer* from KDE's desktop panel, or the command line of an X terminal window like this:

```
$ korganizer &
```

After you press Enter, you will see its main window, as shown in Figure 12.7.

Although the default view is of the current day's to-do list, you can use a different view by clicking on an associated icon in *korganizer*'s graphic toolbar, or use the view menu to see a work week, weekly, or monthly calendar. Use the **Actions** menu to set a new event, such as an appointment, by clicking on the **New Event** menu item. You will then see a dialog box, as shown in Figure 12.8, in which you can enter the particulars.

You can use *korganizer* to set up group meetings, broadcast advisories to members on a category's list, and track progress of tasks. To learn more about *korganizer*, use its built-in help, available through its reference manual (accessed by choosing the **Contents** menu item on the main window's **Help** menu).

![](img/1ea833f5a3e3c1547e3dd2891f52804a_300_0.png)

**Figure 12.7** The KDE korganizer client presents your appointments, events, and to-dos in a variety of views, such as a monthly calendar.

![](img/1ea833f5a3e3c1547e3dd2891f52804a_300_1.png)

**Figure 12.8** The korganizer client provides for appointments, alarms and reminders, and address book e-mails during your X sessions.

> By the time you read this, KOrganizer 2.1 should be ready for release. This new version will have many improvements, including the ability to publish data over an intranet or on the World Wide Web by automatically generating Web pages from your data. See "Resources" at the end of this chapter for the `korganizer` home page.

### Using the GNOME Calendar

The GNOME calendar client, `gnomecal`, is a graphical calendar and organizer much like `korganizer`. You can launch this organizer from the GNOME desktop's panel or the command line of an X terminal window like this:

```
$ gnomecal &
```

After you press Enter, you will see the main `gnomecal` window, as shown in Figure 12.9. To create a new appointment, click the **New** button in the `gnomecal` iconic toolbar. You will then see a dialog box, as shown in Figure 12.10, which you can use to set appointments. The `gnomecal` client also features a to-do list for tracking tasks, and offers various views of your calendar and appointments.

![](img/1ea833f5a3e3c1547e3dd2891f52804a_301_1.png)

**Figure 12.9** The `gnomecal` calendar is a GNOME-compliant client that helps put a little organization in your life by tracking your schedule.

![](img/1ea833f5a3e3c1547e3dd2891f52804a_302_0.png)

**Figure 12.10** One-time or recurring appointments may be entered into the gnomecal calendar using its new appointment dialog box.

To get more help with using gnomecal, use its built-in help to read its reference manual (accessed through the Help menu on the main window).

## Simple Database Clients

This section introduces a simple database client you can use for addresses or business cards and provides a gentle introduction to more sophisticated, serious, and perhaps enterprise-level database systems you will find included with Linux.

### Using the gnomecard Client

The gnomecard client is a deceptively simple, yet feature-filled, address book that creates vCards, or electronic business cards in a text database in your home directory under the .gnome directory. You can launch this client from the GNOME desktop's panel or the command line of an X terminal window like this:

```
$ gnomecard &
```

After you press Enter, you will see the main gnomecard window, as shown in Figure 12.11.

![](img/1ea833f5a3e3c1547e3dd2891f52804a_303_0.png)

**Figure 12.11** The gnomecard client builds a database/address book of your contacts in vCard format.

### What Is a vCard?

A vCard is the file format of an electronic business card, used by PDAs (Personal Data Assistants), PIMs (Personal Information Managers), Web browsers, newer cell phones, and e-mail clients. Defined by the specifications from the Internet Mail Consortium and the IETF (Internet Engineering Task Force), the vCard Specification allows for encapsulation of name, address, phone, e-mail address, Universal Resource Locator (URL), graphics, multimedia, and geographic and time zone information. If you have a Palm PDA and have beamed a business card, then you have used a vCard. The formal specifications are contained in RFC 2425, MIME Content-Type for Directory Information, and RFC 2426, (which is the vCard MIME Directory Profile).

To get started, click the Add button on the gnomecard button toolbar, then start filling out information in its entry dialog boxes, as shown in Figure 12.12.

### Introduction to Advanced Database Systems

There is not room in this chapter or the entire book to fully cover the myriad of advanced RDBMS (Relational Database Management Systems) software available for Linux. You will find two systems most often included with a Linux distribution are MySQL and PostgreSQL. These open source SQL (Structured Query Language) database servers consist of a server daemon and a host of supporting commands and clients, which you can use to build and query sophisticated databases running under Linux.
