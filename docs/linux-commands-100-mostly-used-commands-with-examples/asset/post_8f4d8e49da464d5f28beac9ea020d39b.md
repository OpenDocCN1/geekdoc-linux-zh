
4. Display network statistics at 2-second intervals, 4 times:

```
sar -n DEV 2 4
```

5. Display all available statistics at 30-second intervals, 10 times:

```
sar -A 30 10
```

## 41. echo: Display a message or write a message to a file.

The `echo` command in Linux is used to display a line of text or a string of characters on the standard output (usually the terminal). It is a simple and frequently used command for printing information, variables, or messages to the screen.

**Examples:**

- 1. **Basic Usage:**

```
echo "Hello, World!"
```

- 2. **Using Variables:**

```
name="mohan"
echo "My name is $name"
```

- 3. **Without Newline:**

```
echo -n "This is on the same line"
echo " but this is on the next line."
```

- 4. **Escape Characters:**

```
echo -e "This is a line with a\tab."
```

## 42. history: Display the command history.

The Linux command history is a feature that allows users to view and recall previously executed commands in the terminal. It helps users save time by avoiding the need to retype frequently used commands. The command history is stored in a file, typically located in the user's home directory, and is managed by the shell.

**Examples:**

- 1. **Viewing Command History:**

```
history
```

This will show a numbered list of commands with the most recent at the bottom.

- 2. **Executing Previous Commands:**

```
!5
```

This will execute the command at line 5 of the history.

- 3. **Clearing Command History:**

```
history -c
```

This will not remove the history file; it just clears the current session's history.

## 43. iostat: Report CPU and I/O statistics.

The `iostat` command in Linux is used to report CPU and input/output (I/O) statistics for devices, partitions, and NFS (Network File System). It provides a comprehensive overview of system performance, helping users identify potential bottlenecks and monitor resource utilization.

**Examples:**

- 1. **Display CPU utilization statistics:**

```
iostat -c
```

- 2. **Display device utilization statistics with a 2-second interval for 5 reports:**

```
iostat -d 2 5
```

- 3. **Display extended statistics for devices and partitions in megabytes per second:**

```
iostat -x -m
```

- 4. **Display NFS statistics with timestamps:**

```
iostat -N -t
```

## 44. fuser: Identify processes using files or sockets.

The `fuser` command in Linux is used to identify processes that are using a specific file, file system, or socket. It displays the process IDs (PIDs) of the processes that have a file open, allowing you to determine which processes are accessing a particular resource.

**Examples:**

- 1. **To find which processes are using a specific file:**

```
fuser myfile.txt
```

- 2. **To find processes using a mounted file system:**

```
fuser -m /mnt/myfilesystem
```

- 3. **To kill processes using a file:**

```
fuser -k myfile.txt
```

- 4. **To find processes using a network socket (e.g., port 8080):**

```
fuser -n tcp 8080
```

- 5. **To display more detailed information:**

```
fuser -v myfile.txt
```

## 45. ln: Create links between files.

The `ln` command in Linux is used to create links between files or directories. It has two primary forms: creating hard links and symbolic (soft) links.

**Examples:**

- 1. **Creating a Hard Link:**

```
ln file1.txt hardlink.txt
```

This creates a hard link named `hardlink.txt` pointing to the same inode as `file1.txt`.

- 2. **Creating a Symbolic Link:**

```
ln -s /path/to/file1.txt symlink.txt
```

This creates a symbolic link named `symlink.txt` pointing to `file1.txt`.

- 3. **Creating Symbolic Link with Relative Path:**

```
ln -s -r /path/to/file1.txt relative_symlink.txt
```

This creates a symbolic link named `relative_symlink.txt` with a relative path to `file1.txt`.

- 4. **Prompt before Overwriting:**

```
ln -i file1.txt hardlink.txt
```

If `hardlink.txt` already exists, the command will prompt before overwriting it.

- 5. **Verbose Output:**

```
ln -v file1.txt hardlink.txt
```

Prints a message for each hard link created.

- 6. **Forcefully Creating a Symbolic Link:**

```
ln -sf /path/to/new_target symlink.txt
```

This forcefully creates a symbolic link, overwriting `symlink.txt` if it already exists.

## 46. ldconfig: Configure dynamic linker run-time bindings.

The `ldconfig` command in Linux is used to configure the dynamic linker runtime bindings. It updates the shared library cache, which is a system-wide index of shared libraries. This cache is used by the dynamic linker to quickly locate and load shared libraries when an executable is run.

**Examples:**

- 1. **To update the shared library cache:**

```
sudo ldconfig
```

- 2. **To show what would be done without actually updating the cache:**

```
ldconfig -n
```

- 3. **To clear the entire dynamic linker cache:**

```
sudo ldconfig -X
```

- 4. **To update the cache with verbose output:**

```
sudo ldconfig -v
```

- 5. **To print configuration variables:**

```
ldconfig -C
```

## 47. curl: Transfer data to or from a server.

`curl` (short for "Client for URLs") is a command-line tool used in Unix and Linux systems to transfer data with URLs. It supports various protocols like HTTP, HTTPS, FTP, FTPS, SCP, SFTP, LDAP, and more. `curl` is highly flexible and versatile, allowing users to perform a wide range of tasks, including downloading files, sending requests to web services, and more.

**Examples:**

- 1. **Simple GET Request:**

```
curl https://www.example.com
```

- 2. **Save Output to a File:**

```
curl -o output.html https://www.example.com
```

- 3. **HTTP POST Request with Data:**

```
curl -X POST -d "param1=value1&param2=value2" https://www.example.com/api
```

- 4. **Setting Custom Headers:**

```
curl -H "Authorization: Bearer <token>" https://api.example.com/data
```

- 5. **Follow Redirects:**

```
curl -L https://www.example.com
```

## 48. lsof: List open files and the processes that opened them.

The `lsof` command in Linux is used to list information about files that are currently opened by processes. It provides detailed information about files, directories, and network sockets that are being used by running processes on the system. This can be extremely useful for system administrators and users to troubleshoot issues related to file access, identify which processes are using specific files, or to find out what network connections a particular process has open.

**Examples:**

- 1. **List all open files:**

```
lsof
```

- 2. **List open files for a specific process (e.g., process ID 1234):**

```
lsof -p 1234
```

- 3. **List open files for a specific user (e.g., user 'username'):**

```
lsof -u username
```

- 4. **List open files for a specific command (e.g., command 'nginx'):**

```
lsof -c nginx
```

- 5. **List open network connections:**

```
lsof -i
```

- 6. **List open files for a specific process and display only the process IDs:**

```
lsof -p 1234 -t
```

## 49. iotop: Monitor I/O usage of processes.

`iotop` is a command-line utility on Linux systems that allows users to monitor and display input/output (I/O) usage information of processes in real-time. It provides a dynamic and interactive view of the I/O activities on the system, helping users identify processes that are reading from or writing to storage devices.

**Examples:**

- 1. **Run `iotop` with default settings:**

```
iotop
```

This will display a real-time, interactive view of I/O usage.

- 2. **Run `iotop` in batch mode, with a limited number of iterations and a delay of 2 seconds between each iteration:**

```
iotop -b -n 5 -d 2
```

This runs `iotop` in batch mode, capturing I/O statistics for 5 iterations with a 2-second delay between each iteration.

- 3. **Display only processes or threads actually performing I/O:**

```
iotop -o
```

This will show only the processes or threads that are currently involved in I/O operations.

## 50. rsync: Synchronize files and directories between two locations.
