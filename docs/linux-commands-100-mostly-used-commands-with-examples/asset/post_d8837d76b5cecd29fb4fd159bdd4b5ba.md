
2. Display disk space usage in human-readable format:

```
df -h
```

3. Show total disk space usage:

```
df --total
```

4. Display information for a specific file system (e.g., /dev/sda1):

```
df /dev/sda1
```

5. Display inode information for a file system:

```
df -i
```

## 18. du: Show the size of a directory and its subdirectories.

The `du` command in Linux is used to estimate file and directory space usage. It calculates the size of a directory and its subdirectories, displaying the disk space usage in a human-readable format.

### Examples:

- 1. **Display the disk usage of a directory:**

  ```
  du -h /path/to/directory
  ```

- 2. **Display the total disk usage of a file or directory:**

  ```
  du -sh /path/to/file_or_directory
  ```

- 3. **Display the total disk usage of multiple directories and subdirectories:**

  ```
  du -h --max-depth=1 /path/to/directory1 /path/to/directory2
  ```

- 4. **Display the total disk usage of the current directory and its subdirectories:**

  ```
  du -h --max-depth=1
  ```

- 5. Display the total disk usage of all files and directories, and show the grand total at the end:

  ```
  du -h -c /path/to/directory1 /path/to/directory2
  ```

## 19. tar: Create or extract tar archives.

The `tar` command in Linux is used for creating and manipulating archive files. It stands for "tape archive" and is commonly used to bundle multiple files and directories into a single archive file. The `tar` command is particularly useful for compressing and backing up data.

### Examples:

- 1. **Create a Tar Archive:**

  ```
  tar -cvf archive.tar file1.txt file2.txt directory/
  ```

  This command creates a tar archive named `archive.tar` containing `file1.txt`, `file2.txt`, and the contents of the `directory/`.

- 2. **Extract Files from Tar Archive:**

  ```
  tar -xvf archive.tar
  ```

  This command extracts the contents of the `archive.tar` file.

- 3. **Create a Gzipped Tar Archive:**

  ```
  tar -czvf archive.tar.gz directory/
  ```

  This creates a compressed tar archive named `archive.tar.gz` of the `directory/` using gzip compression.

- 4. **Extract Files from Gzipped Tar Archive:**

  ```
  tar -xzvf archive.tar.gz
  ```

  This extracts the contents of the compressed `archive.tar.gz` file.

- 5. **List Contents of Tar Archive:**

  ```
  tar -tvf archive.tar
  ```

  This command lists the contents of the `archive.tar` file without extracting them.

## 20. wget: Download files from the internet.

`wget` is a command-line utility for downloading files from the internet. It supports downloading via HTTP, HTTPS, and FTP protocols. It is a powerful tool with various options and capabilities for retrieving content from web servers.

### Examples:

- 1. **Basic Usage**:

  ```
  wget https://example.com/file.zip
  ```

  This command downloads the file.zip from the specified URL.

- 2. **Save with a Different Name**:

  ```
  wget -O newfile.zip https://example.com/file.zip
  ```

  Downloads the file from the URL but saves it as `newfile.zip`.

- 3. **Download in the Background**:

  ```
  wget -b https://example.com/largefile.zip
  ```

  Downloads the file in the background, allowing you to continue using the terminal.

- 4. **Recursive Download**:

  ```
  wget -r -np https://example.com/directory/
  ```

  Downloads all files from the specified directory recursively but does not ascend to the parent directory (`-np`).

- 5. **Limit Download Speed**:

  ```
  wget --limit-rate=200k https://example.com/largefile.zip
  ```

  Limits the download speed to 200 kilobytes per second.

- 6. **Resume Interrupted Download**:

  ```
  wget -c https://example.com/largefile.zip
  ```

  If the download is interrupted, use `-c` to resume and complete the download.

## 21. ssh: Connect to a remote server securely.

The `ssh` command, which stands for "Secure Shell," is a widely used protocol for securely connecting to a remote server or device over a network. It provides a secure encrypted communication between two systems, allowing users to access and manage remote systems as if they were local. The `ssh` command is commonly used in Unix-like operating systems, including Linux.

### Examples:

- 1. **Basic SSH Connection:**

  ```
  ssh username@remote-host
  ```

  This command establishes an SSH connection to the remote host with the specified username.

- 2. **Specifying a Port:**

  ```
  ssh -p 2222 username@remote-host
  ```

  Connects to the remote host using port 2222. The default SSH port is 22.

- 3. **Executing a Command:**

  ```
  ssh username@remote-host ls -l /path/to/directory
  ```

  Connects to the remote host and executes the `ls -l /path/to/directory` command, displaying a detailed list of files in the specified directory.

- 4. **Identity File (Private Key):**

  ```
  ssh -i /path/to/private-key username@remote-host
  ```

  Specifies the path to the private key file for authentication. Useful when using key-based authentication instead of a password.

- 5. **Tunneling (Port Forwarding):**

  ```
  ssh -L 8080:localhost:80 username@remote-host
  ```

  Sets up local port forwarding, redirecting traffic from port 8080 on the local machine to port 80 on the remote host.

- 6. **X11 Forwarding:**

  ```
  ssh -X username@remote-host
  ```

  Enables X11 forwarding, allowing the remote server to display graphical applications on the local machine.

## 22. scp: Securely copy files between local and remote machines.

`scp` stands for Secure Copy Protocol, and it is a command-line tool used in Linux and Unix-like operating systems to securely copy files and directories between hosts. It uses SSH (Secure Shell) for data transfer and provides encryption and authentication.

### Examples:

- 1. **Copy a file from local to remote host:**

  ```
  scp file.txt username@remote_server_ip/path/to/destination/
  ```

  Replace `file.txt` with the name of the file you want to copy, `username` with the username on the remote server, `remote_server_ip` with the IP address of the remote server, and `/path/to/destination/` with the destination path on the remote server.

- 2. **Copy a file from remote to local host:**

  ```
  scp username@remote_server_ip/path/to/file.txt /local/path/
  ```

  This command copies the `file.txt` from the remote server to the local machine. Adjust the paths and username accordingly.

- 3. **Copy an entire directory from local to remote host:**

  ```
  scp -r my_directory username@remote_server_ip:/path/to/destination/
  ```

  The `-r` option is used to copy directories recursively.

- 4. **Copy from remote to local with a specific port:**

  ```
  scp -P 2222 username@remote_server_ip:/path/to/file.txt /local/path/
  ```

  Here, the `-P` option specifies the port number (2222 in this example).

- 5. **Copy with compression:**

  ```
  scp -C file.txt username@remote_server_ip:/path/to/destination/
  ```

  The `-C` option enables compression during the transfer.

## 23. find: Search for files in a directory hierarchy.

The `find` command in Linux is a powerful and versatile tool used to search for files and directories in a directory hierarchy based on various criteria.

### Examples:

- 1. **Basic Usage:**

  ```
  find /path/to/search -name "filename.txt"
  ```

  This command searches for a file named "filename.txt" in the specified path.

- 2. **Case-Insensitive Search:**

  ```
  find /path/to/search -iname "file*.txt"
  ```

  The `-iname` option performs a case-insensitive search for files matching the specified pattern.

- 3. **Search by File Type:**

  ```
  find /path/to/search -type f
  ```

  This command finds regular files in the specified path.

- 4. **Search by Directory Type:**

  ```
  find /path/to/search -type d
  ```

  This command finds directories in the specified path.

- 5. **Search for Files Modified in the Last N Days:**

  ```
  find /path/to/search -mtime -7
  ```

  This command finds files modified within the last 7 days.

- 6. **Search for Files Larger Than a Specific Size:**

  ```
  find /path/to/search -size +1M
  ```

  This command finds files larger than 1 megabyte.

- 7. **Execute Command on Found Files:**

  ```
  find /path/to/search -name "*.log" -exec rm {} \;
  ```

  This command finds all files with a ".log" extension and removes them using the `rm` command.

- 8. **Combine Multiple Criteria with Logical Operators:**

  ```
  find /path/to/search -name "*.txt" -o -name "*.md"
  ```
