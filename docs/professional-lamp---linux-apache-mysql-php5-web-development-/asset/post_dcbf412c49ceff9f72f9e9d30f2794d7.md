
# Chapter 3

This is equivalent to:

```php
foreach($array as &$value)
{
    $value = do_something_fancy($value);
}
```

In the former case, there is a brief moment after the `array_map()` has been evaluated when there are two entire arrays. Following the assignment, of course, the previous version of the array is discarded and memory retrieved, but that doesn't happen until the assignment has been completed, and the number of references to the original has decreased to zero. If the array is large, the extra space required can be significant, with large chunks of memory being allocated and then a short time later other large chunks of memory being deallocated. Naturally, if the output array is going into a different variable than the input array, the deallocation doesn't happen, and the one-off economy-sized allocation carried out by the array function's implementation may well be more efficient than the piecemeal element-by-element activity that occurs in `$new_array[] = do_something_fancy($value);`. Clearly, `array_filter()`, `array_udiff()`, and other functions that can output arrays shorter than their inputs ought to be applied prior to those that can't when possible, as it gives those later functions less work to do.

If there are a series of `array_*`-type functions that return arrays, each using the results of the previous, this bulk to-and-fro can become quite tedious for both PHP's memory management and the operating system. It can be obviated to some extent (but only some extent) by writing something like this:

```php
array_walk(
    $array_map(
        'do_something_fancy',
        array_filter(
            array_map('nothing_fancy', $array),
            'purge')
        ),
    'traverse', 'sideways');
```

Instead of this:

```php
$array = array_map('nothing_fancy', $array);
$array = array_filter($array, 'purge');
$array = array_map('do_something_fancy', $array);
array_walk($array, 'traverse', 'sideways');
```

But no one is going to believe you if you say that the former is easier to read. If nothing else, the functions appear in the reverse order that they are applied. Admittedly, it does not help appearances that there does not appear to be any consistency in the order in which arguments are passed to the functions. The best you can say about it is that it helps suppress errors at runtime — if you accidentally mistype `array_map` instead of `array_filter`, PHP would complain at runtime that the “first argument, ‘Array’ , should have been NULL or a valid callback.”

# glob()

A task you may often find yourself doing is reading through a directory for files with names matching a certain pattern — all the text files, for example, or image files. This can be simpler than storing the files in the filesystem, maintaining a list of those files elsewhere, and then having to keep the two synchronized.

And it’s possible that other types of files are in the same directory. This is such a common task that any shell interface provides “globbing” — you can list `*.png`, delete `temp_*`, and so forth. Prior to PHP 4.3, the typical method of achieving the same effect would have used `readdir()` and, based on the examples of that function’s use given in the manual, ended up with something that looks like this:

```php
$filelist = array();
if ($handle = opendir('directory'))
{
    while (false !== ($file = readdir($handle)))
    {
        if (substr($file, -4) == '.txt')
        {
            $filelist[] = $file;
        }
    }
    closedir($handle);
}
```

PHP 5 introduces `scandir()`, which encapsulates the whole `opendir()`/`readdir()`/loop/`closedir()` business, leaving the job of filtering the filenames until afterwards, which in this example could be handled by `preg_grep()` like this:

```php
$filelist = preg_grep('/^\.[txts]*$/', scandir('directory'));
```

But since PHP 4.3, even this is unnecessarily complicated. By using the same shell-like globbing syntax, where `?` represents “any single character” and `*` represents “any string,” you can use the same syntax that you use in the shell to do the same filtering of file names. `$filelist = glob("*.txt", *directory*);`

The `glob()` function has a few optional flags that can be bitwise-ORed together to adjust the behavior of the function. For example, if the directory in question had a mix of JPEG and PNG files (along with a miscellaneous scattering of other types, and of course the inevitable `.` and `..` directories), the `GLOB_BRACE` flag can be set, and the alternative glob patterns for identifying those files by their extensions passed to `glob()` as a comma-separated list in braces:

```php
$filelist = glob("{*.jpg,*.jpeg,*.png}", *directory*, GLOB_BRACE);
```

# PHP Streams

Starting with PHP 4.3, PHP’s URL wrappers (the things that allow you to use URLs in places where file-names are usually expected) has been extended to become the basic mechanism of file interaction in general. One of the consequences of this is that you can now use URLs in almost any context where a local file path would be appropriate. (Some specialized aspects, such as configuration settings, are exempt from this: you can’t have a URL in your include path, for example.) This includes file access functions used by third-party extensions, with PHP now treating local file accesses as requests via `file://` URLs.

The other consequence is that it became feasible in PHP 5 to expose an interface for constructing custom stream wrappers to the PHP developer in the so-called streams interface.

Programmers who are familiar with Java or C++ will already be familiar with the streams concept; the kioslaves that appear in the K Desktop Environment are another example. In PHP, a stream is an object that behaves like a file — you may be able to read bytes from it, write bytes to it, go to a particular byte position within it, ask how many bytes there are, and so on. Note the use of “may be” — just as some files are read-only and some are write-only, streams too can be read-only or write-only, while some generate their data on the fly so that there is no clearly defined analog of “file offset” or “file size” or even “end of file.” The idea is that users of a stream never have no idea just how the data they work with is stored or handled; they just read and write. The most significant limitation, compared with, say, Java, is that PHP streams are all byte streams. To stream something else — objects in particular — you need serialization to convert it into something that will go through a stream. This is PHP’s loose typing having an effect once again: since every stream is a byte stream, any stream can be used anywhere (whether it makes sense or not).

# Creating and Using Streams

Building a stream wrapper is simply a matter of adding certain methods to the stream object, and using `stream_wrapper_register()` to identify it as a wrapper.

`stream_wrapper_register()` is called with two arguments. The first is the *protocol*, which is simply a name that indicates the wrapper to be used when a stream is to be opened — what is known in URLs as the *scheme*. It’s the bit in the URL before the `//`, that is, the `http` of HTTP URLs, the `ftp` of FTP URLs, and the `file` of file URLs. For example, if you implement a stream and register it with a protocol of `foonily`, you will then be able to `go fopen(“foonily://…”, “r”)` to enable reading from a foonily stream. The default protocol used by `fopen()` and the other filesystem functions is `file`, which is why you hardly ever see `file://path/file.ext`, because `path/file.ext` has the same effect.

The second argument is a string containing the name of the class that implements your wrapper.

Naturally, the full list of wrapper methods are given in the manual. The principal ones are as follows:

-   * `stream_open()` : This function contains startup code for a new stream — initializing variables, opening streams of its own, and so forth. You call this function with four arguments. The first two are the same path and mode values as the corresponding `open()` call. (For third-party extensions, the appropriate options will be worked out and provided.) The third argument could contain up to two flags: `STREAM_USE_PATH` indicates that you should search `include_path` if necessary to find the specified file, and `STREAM_REPORT_ERRORS` dictates whether it is the stream’s responsibility to trigger any errors if the stream cannot be opened or something else goes wrong, or whether such things are going to be handled higher up (in which case your stream should not report any errors). `STREAM_USE_PATH` is only relevant if you actually are looking for something in the local filesystem, whether it is the file requested, or an auxiliary file that your stream uses. If your stream is read-only, it should return `FALSE` (and possibly trigger a warning) if the requested mode is for writing (`w`, `a`, `r+`, `a+`), and similarly for write-only streams.

> The PHP manual mentions “fopen_with_path()”, but as of 5.0.3 this function doesn’t exist. The `include_path` configuration setting is of course available via `ini_get()`.

-   * `stream_read()` : If the stream cannot be read, this should return `FALSE`. Otherwise it should return at most the number of bytes requested. As the wrapper’s author, it is your responsibility to ensure that any relevant state, including any file pointers, is maintained between successive calls to this method. You are allowed to return fewer bytes than requested (although an empty string may be interpreted as indicating the end of the stream).
