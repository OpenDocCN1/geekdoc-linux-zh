+   - Layout Policies  
+   - Tab Widgets and Stacked Widgets  
+   - Splitters  
+   - Single Document Interface (SDI)  
+   - Multiple Document Interface (MDI)

# # Layouts and Multiple Documents

In every dialog we have created so far, all the widgets have been visible at the same time. But in some cases, such as, complex configuration dialogs or property editors, so many widgets are required that showing them all at once could confuse the user. For such situations we can use tab widgets or stacked widgets that allow us to group related widgets together, and show only the relevant group, or we can use extension dialogs that can show extra options on demand. These techniques can help make dialogs smaller and easier for users to navigate and use; we will cover them in this chapter’s second section.

In the main-window-style applications we have created, we had one central widget. But in some situations, we need to show two or more widgets in the central area, and often want to give the user some control over their relative sizes. One way to achieve this is to use a single central widget with dock windows; we saw this approach in Chapter 6. Another approach is to use splitters, the subject of this chapter’s third section.

Another issue that arises with main-window-style applications is how we deal with multiple documents. There are four main approaches to this. One is to use multiple instances of the application. In this approach, the user launches one instance of the application for each document they wish to work on. In theory this requires no programming effort at all, but in practice, we might want to implement some kind of file-locking scheme or use interprocess communication to ensure that the user does not start the application two or more times on the same document. All the applications we have created so far are of this kind, although none of them has used file locking.*

A second approach is to use SDI (Single Document Interface). This means that the user is expected to run only one instance of the application, but can use that application instance to create as many main windows as they need to handle all the documents they wish to work on. (It is possible to ensure that the user can only have one instance of an application running at the same

*For file-locking code, see “File Locking Using a Cross-Platform API” in the Python Cookbook.

269