

```sh
# Ready! Let's copy the specified files.

cp -p -v "$@" "$dropbox/$targetdir"
fi

# Now let's launch the Dropbox app to let it do the actual sync, if needed.
exec startdropbox -s
```

Listing 13-3: The syncdropbox script

## How It Works

The vast majority of Listing 13-3 is testing for error conditions, which is tedious but useful for ensuring that the script is invoked properly and isn’t going to mess anything up. (We don’t want any lost data!)

The complexity comes from the test expressions, like the one at ❶. This tests whether the destination directory for a directory copy $sourcedir in the Dropbox folder is a file (which would be weird) or an existing directory. Read it as “if exists-as-a-file $dropbox/$sourcedir OR exists-as-a-directory $dropbox/$sourcedir, then . . .”

In the other interesting line, we invoke cp ❷ to copy individually specified files. You might want to read the cp man page to see what all those flags do. Remember that $@ is a shorthand for all the positional parameters specified when the command was invoked.

## Running the Script

As with many of the scripts in this book, you can invoke this without arguments to get a quick refresher in how to use it, as Listing 13-4 demonstrates.

```sh
$ syncdropbox
Usage: syncdropbox [-d source-folder] {file, file, file}
```

Listing 13-4: Printing the usage for the syncdropbox script

## The Results

Now in Listing 13-5, let’s push a specific file to be synchronized and backed up to Dropbox.

```sh
$ syncdropbox test.html
test.html -> /Users/taylor/Dropbox/sync/test.html
$
```

Listing 13-5: Syncing a specific file to Dropbox

Easy enough, and helpful when you recall that this makes the specified files—or directory full of files—easily accessible from any other device that’s logged in to your Dropbox account.

## Hacking the Script

When a directory is specified but already exists on Dropbox, it would be far more useful to compare the contents of the local and Dropbox directories than to just print an error and fail. Additionally, when specifying a set of files, it would be very useful to be able to specify the destination directory in the Dropbox file hierarchy.

> **OTHER CLOUD SERVICES**
> 
> Adapting these first two scripts for Microsoft's OneDrive service or Apple's iCloud service is fairly trivial, as they all have the same basic functionality. The main difference is naming conventions and directory locations. Oh, and the fact that OneDrive is OneDrive in some contexts (like the app that needs to be running) and SkyDrive in other contexts (the directory that's in your home directory). Still, all easily managed.

## #91 Creating Slide Shows from Cloud Photo Streams

Some people love the iCloud photo backup service Photo Stream, while others find its tendency to keep a copy of every photo taken—even the throwaway junker photographs from mobile devices—annoying. Still, it's pretty common to sync photos with a favorite cloud backup service. The drawback is that these files are essentially hidden—because they're buried deep in your filesystem, they won't be automatically picked up by many photo slide show programs.

We'll make this better with slideshow, a simple script (shown in Listing 13-6) that polls the camera upload folder and displays the pictures therein, constrained to specific dimensions. In order to achieve the desired effect, we can use the display utility that's shipped with ImageMagick (a suite of powerful utilities you'll learn more about in the next chapter). On OS X, the brew package manager user can install ImageMagick easily:

```
$ brew install imagemagick --with-x11
```

> **NOTE**
> 
> A few years ago, Apple stopped shipping X11, a popular Linux and BSD graphics library, with their main operating system. In order to use the slideshow script on OS X, you'll need to provide ImageMagick with the X11 libraries and resources that it requires by installing the XQuartz software package. You can find more information about XQuartz and how to install it on the official website: https://www.xquartz.org/.

