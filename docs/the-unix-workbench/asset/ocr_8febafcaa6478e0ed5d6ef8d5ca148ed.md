```
alias docs='cd ~/Documents'
alias edbp='nano ~/.bash_profile'
```

The first alias creates a new command docs. Now entering docs into the command line is the equivalent of entering cd ~/Documents into the comamnd line. Open let’s edit our ~/.bash_profile with nano. If there’s anything in your ~/.bash_profile already then start adding lines at the end of the file. Add the line alias docs='cd ~/Documents', then save the file and quit nano. In order to make the changes to our ~/.bash_profile take effect we need to run source ~/.bash_profile in the console:

```
source ~/.bash_profile
```

Now let’s try using docs:

```
docs
pwd
```

```
## /Users/sean/Documents
```

It works! Setting different aliases allows you to save time if there are long commands that use often. In the example ~/.bash_profile above, the second line, alias edbp='nano ~/.bash_profile' creates the command edbp (edit bash profile) so that you can quickly add aliases. Try adding it to your ~/.bash_profile and take your new command for a spin!

There are a few other details about the ~/.bash_profile that are important when you’re writing software which we’ll discuss in the Bash Programming chapter.