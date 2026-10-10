```
```
document.getElementById("info-selection").innerText = message;
});
```
```

And the code to include in your C# back-end.

```
```
Electron.IpcMain.On("information-dialog", async (args) =>
{
    var options = new MessageBoxOptions("This is an information dialog. Isn't it nice?")
    {
        Type = MessageBoxType.Info,
        Title = "Information",
        Buttons = new string[] { "Yes", "No" }
    };

    var result = await Electron.Dialog.ShowMessageBoxAsync(options);

    var mainWindow = Electron.WindowManager.BrowserWindows.First();
    Electron.IpcMain.Send(mainWindow, "information-reply", result.Response);
});
```
```

There are many types of native dialog windows available (other than the one described above), you can review in detailed the code of the dialog.cs file for having more examples of how you should use this feature.

This is only a few of the features illustrated in the example application, but it seems that they are the most exotic part from the web application developer's point of view.