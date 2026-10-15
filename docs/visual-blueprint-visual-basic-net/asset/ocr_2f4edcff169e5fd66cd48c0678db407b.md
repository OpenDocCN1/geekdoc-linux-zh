# VISUAL BASIC .NET

# WATCH FOR FILE SYSTEM CHANGES

The Windows Explorer immediately updates whenever a file saves onto disk. The Windows subsystem allows programs to request notification when certain directories update. You can receive events using the FileSystemWatcher class when file system changes occur on a particular drive or directory.

You can create an instance of the FileSystemWatcher class or you can add the FileSystemWatcher to a Windows Form from the Component category of the Toolbox. This topic assumes you use the Windows Form component because of the simplicity it adds through the visual interface.

The Path property specifies what drive or directory the component monitors for changes. Set IncludeSubdirectories to include any directories under the specified Path. The EnableRaisingEvents property enables or disables the component's notification events.

The component provides four events that fire when file system changes occur: Changed, Created, Deleted, and Renamed. For more information on events in Windows Forms, see Chapter 2.

The Changed event fires when an attribute of a file changes such as the file size, last modified date, and last viewed date. You alter the NotifyFilter property to set conditions for when the Changed event fires. For example, set NotifyFilter to LastWrite to have a component fire only when an application writes to a file.

The Created event fires when a new file or directory appears in the file system. The Deleted event fires when the user removes a file or directory from the file system, and the Renamed event fires when a file or directory name changes.

Each of the events passes a FileSystemEventArgs object as variable e to your event handler. The object includes a property Name that specifies the name of the file or directory of the change relative to the specified Path. The property FullName returns the entire path. For the Renamed event, the property OldFullName specifies the previous name of the file.

# WATCH FOR FILE SYSTEM CHANGES

![](bbox=[0.07, 0.635, 0.9, 0.82])

+   1. Create a new Windows Application project or open an existing one.
+      This example loads a ListBox control onto the form to display the output.

+   2. In the Toolbox, click the Components category.
+   3. Double-click the FileSystemWatcher component.
+      The component loads into the form's component tray.

+   4. In the Properties window, type the path to watch in the Path property.
+   5. Set any other necessary properties.

+   6. Double-click the FileSystemWatcher in the component tray.