⇒ To create a compressed archive called project.tar.gz from the contents of the project directory, type:
$ tar -zcvf project.tar.gz project [RET]

This command creates a compressed archive file, project.tar.gz, containing the project directory and all of its contents. The original project directory remains unchanged.

NOTES: When you use the -z option, you should specify the archive name with a .tar.gz extension and not a .tar extension, so the file name shows that the archive is compressed. This is not a requirement, but it serves as a reminder and is the standard practice.

# 8.5.2 Listing the Contents of an Archive

To list the contents of a tar archive without extracting them, use tar with the -t option.

⇒ To list the contents of an archive called project.tar, type:
$ tar -tvf project.tar [RET]

This command lists the contents of the project.tar archive. Using the 'code-v option along with the -t option causes tar to output the permissions and modification time of each file, along with its file name—the same format used by the ls command with the -l option (see Recipe 5.3.3 [Listing File Attributes], page 136).

Include the -z option to list the contents of a compressed archive.

⇒ To list the contents of a compressed archive called project.tar.gz, type:
$ tar -ztvf project.tar.gz [RET]

# 8.5.3 Extracting Files from an Archive

To extract (or unpack) the contents of a tar archive, use tar with the -x ("extract") option.

⇒ To extract the contents of an archive called project.tar, type:
$ tar -xvf project.tar [RET]

This command extracts the contents of the project.tar archive into the current directory.

If an archive is compressed, which usually means it will have a .tar.gz or .tgz extension, include the -z option.