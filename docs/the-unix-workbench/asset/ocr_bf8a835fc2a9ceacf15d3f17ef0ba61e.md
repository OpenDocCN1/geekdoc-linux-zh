```
git checkout readme.txt
cat readme.txt
```

```
## Welcome to My First Repo
## Learning Git is going well so far.
```

And as you can see the changes we made to readme.txt have been undone.

# Ignoring Files

Sometimes you might have files that you never want Git to track, for example binary files that are generated as by-products of running code (PDFs or images), or secrets like passwords or API keys. A file in your Git repository called .gitignore can list names of files and sub-folders, or simple regular expressions (whatever you can use with ls) in order to specify files which should never be tracked. Each line of a .gitignore file should specify a file or group of files that should not be tracked by Git. Let’s make a .gitignore file to make sure that we never track image files in this repository:

```
touch toby.jpg
git status
```