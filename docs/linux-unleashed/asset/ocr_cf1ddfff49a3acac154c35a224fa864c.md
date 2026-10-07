Names MUST match upper, lower case exactly. Use the "quotes" as shown. To get a directory, type: DIR. To change directory, type: CD "Dir.Name" To read a short text file, type: GET "File.Name" TT For more, type HELP or see FAQ in gopher. To quit, type EXIT or Control-Z.

230- If you email to info@sunsite.unc.edu you will be sent help =information
230- about how to use the different services sunsite provides.
230- We use the Wuarchie experimental ftpd. if you "get" =>directory>.tar.Z
230- or <file>.Z it will compress and/or tar it on the fly. Using ".gz" =instead
230- of ".Z" will use the GNU zip (/pub/gnu/gzip*) instead, a superior
230- compression method.

Once you are on the remote system, you can use Linux (UNIX) commands to display file contents and move around directories. To display the contents of a directory, use the command ls or the DOS equivalent dir. To change to a subdirectory, use the cd <dir> command. To return to the parent directory (the one above the current directory), use the command cd ... Unlike Linux, there are no keyboard shortcuts available with FTP so you have to type in the names of files or directories in their entirety (and correctly).

As you move through the directories and find a file you want to move to your system, use the FTP get command, as in:
get "file1.txt"

The commands get (download) and put (upload) are relative to your home machine, not to the remote. When you issue a get command, you are telling your system's FTP soft- ware to get a file from the remote machine. A put commands tells FTP to put a file from your local machine onto the remote machine. It is important to remember which com- mand moves in which direction or you could accidentally overwrite files.

The quotation marks around filenames are optional for most versions of FTP, but they do provide specific characters to the remote version (preventing shell expansion). This can prevent error messages from FTP or accidental transfers of many files instead of just one, so quotation marks are a useful practice to employ.

When you issue a get command, the remote system transfers data to your local machine and displays a status message when it is completed. There is no indication of progress during transmission of a large file, so be patient. This is a sample transcript of a get command: