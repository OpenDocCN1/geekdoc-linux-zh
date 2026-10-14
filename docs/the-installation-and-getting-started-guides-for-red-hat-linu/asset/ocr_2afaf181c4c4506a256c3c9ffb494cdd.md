# The Getting Started Guide for Red Hat Linux 6.0

To remove directories with rm, you must specify the -r option.

For example, if you want to recursively remove the directory tigger you would type:

```
rm -r tigger
```

And if you want to combine options, such as forcing a recursive deletion, you can type:

```
rm -rf tigger
```

+   - Tip: Be careful! rm is a powerful command, and can delete your entire system! If you're root and you type the simple command rm -rf / you're sunk — like a snake eating its tail, the command will recursively remove everything on your system.

The safer alternative to using rm for removing directories is the rmdir command. With this command, you won't be allowed to use recursive deletions, so a directory which has files in it won't be deleted.

Read the rmdir man page by typing man rmdir to find out more about the command.

# Time to Learn More

So far, you've learned to become familiar with how to create accounts, using passwords, your filesystem and more.

But what we've covered is just the tip of the iceberg. There are books, websites, and newsgroups (Linux users are second to none when it comes to helping new users) to help you find out more about your new system.

You can begin with the next chapter, in which you'll find pointers to other documentation, as well as additional post-installation configuration.