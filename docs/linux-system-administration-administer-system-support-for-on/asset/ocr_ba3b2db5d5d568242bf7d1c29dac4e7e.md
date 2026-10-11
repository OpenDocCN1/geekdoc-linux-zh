This sets the HTML file directory. If your users have Web space on their user accounts, the Web pages are not stored here.

# UserDir: The name of the directory which is appended onto a user's home directory if a ~user request is received.

UserDir public_html

The users listed in the user directory must have permission 755 before other sites can access their Web pages. If I were to create my own Web page, it would be in the directory /home/stripes/public_html. In that directory, I'd need to have a file called index.html with permission 755. When I've set that up, everyone can see my home page.

If necessary, you can change the name of the directory to almost anything else. Remember, however, that all your users need to have the same directory—with the same permissions listed earlier — in their accounts:

# DirectoryIndex: Name of the file or files to use as a pre-written HTML directory index. Separate multiple entries with spaces.

DirectoryIndex index.html

You may want to add the home.html document since it is still use it today.

# FancyIndexing is whether you want fancy directory indexing or standard

FancyIndexing on

If you want to enhance the look of your indexing, turn on FancyIndexing. An example follows:

```
# AddIcon tells the server which icon to show for different files or filename # extensions

AddIconByEncoding (CMP,/icons/compressed.gif) x-compress x-gzip

AddIconByType (TXT,/icons/text.gif) text/*
AddIconByType (IMG,/icons/image2.gif) image/*
AddIconByType (SND,/icons/sound2.gif) audio/*
AddIconByType (VID,/icons/movie.gif) video/*

AddIcon /icons/binary.gif .bin .exe
AddIcon /icons/binhex.gif .hqx
AddIcon /icons/tar.gif .tar
```