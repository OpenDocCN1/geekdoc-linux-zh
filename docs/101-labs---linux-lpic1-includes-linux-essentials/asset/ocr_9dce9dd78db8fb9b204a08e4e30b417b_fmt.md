
```
sudo dpkg -i [file]
```

Though, again, you would have to also install the dependencies manually first. To remove the package when you're done with it: `dpkg -P [package]`

# Notes

Though `dpkg` is great for information gathering, in practice it is generally better to manage your installed packages through a single central database. That may mean adding a third-party repo, or downloading a package and then manually adding it to Apt.
