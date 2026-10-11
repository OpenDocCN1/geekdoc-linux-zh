
## IN-DEPTH

### GUI Apps with Fyne

Fyne size will be the same across different output devices. The last three lines of the main function become:

```
w.SetContent(loadUI())
w.Resize(fyne.NewSize(200, 280))
w.ShowAndRun()
```

When you run the updated code, you will see the new user interface appear on your screen (Figure 2).

### Listing 5: Storing Data

```
var (
	todos []string
	list *widget.List
)
```

### Listing 6: Adding a To-Do Item via Tapping

```
add := widget.NewButtonWithIcon("",
	theme.ContentAddIcon(),
	func() {
		addTODO(input.Text)
		input.SetText("")
	})
```

### Listing 7: Adding a To-Do Item via the Keyboard

```
input.OnSubmitted = func(item string) {
	addTODO(item)
	input.SetText("")
}
```

### Listing 8: data.go

```
01 package main
02 
03 import "fyne.io/fyne/v2"
04 
05 func addTODO(todo string) {
06 	todos = append(todos, todo)
07 	list.Refresh()
08 }
09 
10 func deleteTODO(todo string) {
11 	for i, text := range todos {
12 		if text != todo {
13 			continue
14 		}
15 
16 		todos = append(todos[:i],
17 			todos[i+1:]...)
18 		break
19 	}
20 	list.Refresh()
21 }
```

### Remembering To-Dos

You want to be able to add items and mark them as done in your app. To do this, you will use a new global variable, todos, which is a slice of strings (denoted as []string). You will manipulate this slice when adding or deleting items, and your list will always draw this data’s current state. First, you add a new todos variable to main.go. You also need to keep a reference to the list variable created earlier so it can be updated (shown in Listing 5).

### Adding Items

When the user taps on the add button created in Listing 3, a new item will be added to the to-do list. To do this, you make a more useful tapped handler for the button. Instead of logging to the console, you will use the code in Listing 6, which asks for a new item to be added and then clears the input text to get ready for another to-do item.

Because some users prefer to run an app from the keyboard, you will also want this functionality when the user hits Return or Enter. Thankfully, the Entry widget has an OnSubmitted callback that you can set as shown in Listing 7.

Both handlers call a new addTODO function, which simply appends a new item to the slice and refreshes the list (see Listing 8).

### Populating the List

Now that you have some data to display, you need to tell the list how to update accordingly. To do this, you add some code to the third callback of the List widget. This code will set the Check widget’s text and make sure that it is not checked (because the list currently only has pending to-do items). Listing 9 achieves this using a replacement callback function.

Line 1 of Listing 9 makes sure you can use the Check widget’s functionality. The list does not know what type of content it displays, so you need to do a type cast to match the widget you created in the second callback function. With this in place, you will see your to-do list – all that is left is to delete them!

### Listing 9: Displaying To-Do Content

```
01 func(id widget.ListItemID,
02 	o fyne.CanvasObject) {
03 	check := o.(*widget.Check)
04 	check.SetChecked(false)
05 	check.Text = todos[id]
06 }
```

### Listing 10: Deleting To-Do Items

```
check.OnChanged = func(done bool) {
	if done {
		return
	}
	deleteTODO(check.Text)
}
```

### Deleting Items

The to-do list is only keeping track of pending items, so you want to remove any to-do item once it is checked. For this, you can set the OnChanged callback to your Check widget (Listing 10), much like you set OnSubmitted on the Entry widget.

The OnChanged callback will be called if the item is checked or unchecked – which is why you first test that it is being marked as completed using the bool parameter. Assuming it should be deleted, you call the helper function deleteTODO from Listing 8.

The method shown in Listing 8 is a little complicated because there is no built-in way to delete an item from a slice in Go. Listing 8 performs “re-slicing,” which sets the to-do list to a join of two other lists (a list for before and one for after the item is deleted). The code then refreshes the list as before, so your item disappears. If you run your app once more, you will see that it is empty, but you can add new items and mark them as done as often as you like, as shown in Figure 3.

### Storing Data

You now have a fully functional app to track your to-do items, but the app will forget the items when you exit. To remedy this, you can connect to a database or store data in a file. However, Fyne lets you store your data in Preferences, a simple key-value store used to easily keep track of user interface state and small data storage without worrying about file storage or connection handling. You can access this feature using the `Preferences()` method on the `App` type created earlier.

### Loading To-Do Items

You need to ensure that any existing to-do items are loaded when the app starts. To do this, you can simply set up the `todos` variable to be the result of a `loadAll`. Immediately before calling `loadUI`, you need to call

```
list = loadTODos(a.Preferences())
```

This call will pass your application preferences to a new `loadTODos` function that will return a slice of all stored to-dos.

### Saving the Data

Before you have data to parse, you need to save it! To do this, you will use another new method, `saveTODos`, which will take the current slice to save and a reference to the preferences you will be using:

```
saveTODos(todos, p)
```

Be sure to call this method inside `deleteTODO` and `addTODO` after updating the data. The methods that actually do the work in this example are really simple – you just concatenate all the items to a single string using a `joiner` constant and then split the items out on `load`, as shown in Listing 11.

### Listing 11: storage.go

```
01  package main
02
03  import "fyne.io/fyne/v2"
04
05  const joiner = ","
06
07  func loadTODos(p fyne.Preferences) []string {
08      all := p.String("items")
09      if all == "" {
10          return []string{}
11      }
12      return strings.Split(all, joiner)
13  }
14
15  func saveTODos(items []string, p fyne.Preferences) {
16      allItems := strings.Join(items, joiner)
17      p.SetString("items", allItems)
18  }
```

### Local Storage or Cloud

Regardless of your operating system or device, Listing 11 will store the data for you. However, many apps now want to have centrally stored information on a cloud service. The great news is that Fyne supports this too! Using exactly the same code from Listing 11, you can have a cloud back end for your data, which is set up by simply calling `SetCloudProvider` in your app with a suitable provider description. You can find more information about setting this up in a recent Fyne-Conf video [3].

### Packaging and Installing

Once you have completed your app, the next step is to make it more readily available either for yourself or others.

First, you need to add an icon before installing or sharing the app.

Although Fyne is a vector graphics-based toolkit, you will need a bitmap image for the app icon. For greatest compatibility, create a 1024x1024 PNG file, name it `Icon.png`, and save it to the project folder. Once created, this will be used as the app icon. The best way to bundle apps is to use the `fyne` command-line tool:

```
> go install fyne.io/fyne/v2/cmd/fyne@latest
```

Once installed you can call `fyne package` to set up an app bundle. It will use the appropriate format for the current operating system. You can also install it at the same time using `fyne install`. This will package the app and put it into your standard app location (`/usr/local/bin` for most Linux distributions).

If you get a “command not found” message, be sure to check that the `Go` binary location (usually `~/.go/bin`) is in your `$PATH`. Once complete, the app will be available in your favorite app launcher (Figure 4).

### Sharing with Others

Before sharing your app, you should consider adding a tutorial for new users. This is really easy for a to-do list app because you can just add items to the UI when the app has not been used before – `GetString` with `GetPreferenceString` `Fallback`. The fallback case will be used when the requested preference key has not previously been saved. Try the following:

![](img/740bd926461af28ed755753238e647a2_44_0.png)
![](img/740bd926461af28ed755753238e647a2_45_0.png)
