
3. 在窗口的右侧窗格中，单击 OpenOffice.org Word Processor 一次，单击 Properties 按钮。然后将出现一个 Launcher Properties 窗口。

4. 在该窗口的 Name 框中，首先将启动器的名称缩短为 Writer 或 Word Processor 或适合你的任何名称。

5. 接下来，单击 Icon 按钮（它上面没有写 Icon，而是显示 Writer 图标）。使用“项目 3A-4：更改面板启动器图标”第 33 页中描述的方法，导航到 `/usr/share/icons/hicolor/48x48/apps` 中的 Choose an icon 窗口。

6. 向下滚动到并单击 `openofficeorg3-writer.png`，然后单击 Open。

7. 新图标现在应该出现在 Launcher Properties 窗口中。单击 Close，你将能够在菜单编辑器窗口中看到更改。

8. 对 OpenOffice.org Spreadsheet 甚至 OpenOffice.org Presentation 重复该过程，如果你喜欢的话。只需确保为每个项目选择合适的名称并选择合适的图标（例如 Spreadsheet 使用 `openofficeorg3-calc.png`，Presentation 使用 `openofficeorg3-impress.png`）。完成后，将编辑器窗口保持打开状态以继续项目 3B-2 的工作。

![](img/f7cef0df22f9dba5a41777808c98eece_76_0.png)

Figure 3-14: Customizing your menus

## 3B-2: Changing the Order of Icons Within Menus

While you still have everything open to the Office menu, let's deal with what I consider to be another problem: the order of the items in the menu. It just doesn't make sense to me to have what is arguably the most commonly used office application, your word processor, way down there at the bottom of the menu.

Remedying this situation is easy. Just click the OpenOffice.org Word Processor icon in the right pane of the menu editor window. Then click the Move Up button on the right side of the window as many times as necessary until the Word Processor icon is right there at the top of the list.

Now that your word processor is up there at the top of the menu, the other OpenOffice.org modules seem a bit out of place down at the bottom, so you might as well move the other OpenOffice.org modules up near the top too by using the same method.

While I'm being logical and all, why not make things even better by getting the Evolution launcher out of the Office menu and moving it over to the Internet menu, which seems a far more natural place for it to be? If you agree and want to hide this instance of Evolution, just uncheck the box next to its name. The name of that entry should then switch to italic typeface, indicating that the item in question will not be visible in the actual drop-down menu. Once you're done, your menu editor window should look something like mine in Figure 3-15.

If all seems fine to you, click Close and then select Applications ▸ Office to check out the results.

![](img/f7cef0df22f9dba5a41777808c98eece_77_0.png)

Figure 3-15: Managing menus with the menu editor

Now add Evolution to the Internet menu by clicking Internet in the left pane of the menu editor window and then clicking the New Item button. In the Create Launcher window that appears, type Evolution Mail and Calendar in the Name box and `evolution` in the Command box. The Evolution icon should then automatically appear in the icon button. Once done, click OK, after which the new Evolution entry will appear in the Internet menu. Close the menu editor window.

## Virtual Desktops

It is now time to discuss a rather convenient feature of Linux: virtual desktops. Although the virtual desktop feature has only recently made its way into other operating systems, it has been a Linux feature for years (yes, it started here, folks). But rather than babble on about what this virtual desktop business is and what it can do for you, it is probably best to have you learn about it by giving you some hands-on experience.

In your GNOME panel, click the Wanda (Fish), OpenOffice.org Writer, and Firefox launchers. You will then have three windows open in your present desktop, or workspace. Now look at the Workspace Switcher to the right of the bottom panel. There should be four boxes, with the one on the left (your present workspace) in light gray. If you click the box next to that, now in dark gray, all your open windows will suddenly disappear.

Actually, nothing has really disappeared—you are just viewing a new desktop. All your other windows are still open and running in the previous desktop.
