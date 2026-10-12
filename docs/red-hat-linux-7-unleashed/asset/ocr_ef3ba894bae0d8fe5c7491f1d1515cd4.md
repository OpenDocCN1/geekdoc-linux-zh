# # The Type of File Field

The type of file field for `/etc/ftpcvconversions` is a list of possible filetypes that can be acted on, with type names separated by the pipe symbol (|). The three file types recognized are `T_REG`, `T_ASCII`, and `T_DIR`, which represent regular files, ASCII files, and directories, respectively. An example of this entry is `T_REG | T_ASCII`.

# # The Options Field

The options field of `/etc/ftpcvconversions` is similar to the type of file field in that it is composed of a list of names separated by the pipe symbol (|). The three types of options supported are `O_COMPRESS`, `O_UNCOMPRESS`, and `O_TAR`, which specify whether the command compresses files, decompresses files, or uses the `tar` command. An example entry is `O_COMPRESS | O_TAR`, which says the file is both compressed and tarred.

# # The Description of the Conversion

The last parameter of `/etc/ftpcvconversions`, the description of the conversion, is a free-form entry in which you can describe the type of conversion.

# # Example of an `/etc/ftpcvconversions` Entry

The following is a sample entry that compresses files using `gzip` on demand. This would allow someone who wants to get the file `orb_disccography.tar` to instead request the file `orb_disccography.tar.gz` and have the server compress the file by using `gzip` before sending it to him. The configuration line that does this is as follows:

```
::: gz:/bin/gzip -9 -c %s::T_REG:O_COMPRESS:GZIP
```

The first two parameters are not necessary because you don’t want to remove anything from the filename before sending it to the requester. The third parameter is empty because you don’t want to add any strings to the beginning of the filename before sending it. The fourth parameter, though, does have the string `.gz`, which adds the `.gz` suffix to the file before sending it. The fifth parameter is the actual command used to compress the file, where the `-9` option tells `gzip` to compress the file as much as it can, `-c` sends the compressed file to the standard output, and `%s` is replaced by the server from which the filename is requested (for example, `orb_disccography.tar`). `T_REG` in the sixth parameter tells the server to treat the file as a normal file rather than an ASCII file or directory. The second-to-last parameter, `O_COMPRESS`, tells the server that the action being taken is file compression. The last parameter is simply a comment for the administrator so he can quickly determine the action being taken.