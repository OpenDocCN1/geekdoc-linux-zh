![](image_rsrcPB.jpg)

# Who I am?

Tomas Gonzalez is a professional with extensive experience in the field of computing. With 5 years of work experience in a computer store, he has developed a deep knowledge of technology-related products and services. During his time at the store, he has gained skills in customer service, problem solving and advice on choosing computer products.

In addition, Tomas has expanded his experience as a web programmer for 2 years, focusing on the PHP language and the use of APIs. As a web programmer, he has worked on web development projects, using APIs to integrate third-party functionality and data into the applications he has created. His experience in this area has allowed him to acquire strong skills in web development, data manipulation and creating technical solutions.

Tomas has also ventured into teaching, working as a trainer and giving private classes. For 1 and a half years, he has shared his knowledge and experience with others, providing personalized training and guiding his students in learning computer concepts and programming.

In summary, Tomas Gonzalez is a professional with experience in the field of computing, standing out as an expert in computer products, a skilled web programmer with experience in PHP and APIs, and a dedicated trainer who shares his knowledge with enthusiasm. His combination of practical experience in a computer store, web development and teaching provides him with a solid foundation to address various challenges in the technology field.

# Introduction

Welcome to "Bash by Examples: Learning by Doing," a book designed to take you by the hand on the exciting journey of becoming a proficient user of the Bash command line. In the computing world, understanding how to efficiently interact with the Unix/Linux shell is not only a valuable skill, but also a necessity for a wide range of IT professionals, from software developers to system administrators and data scientists. .

The philosophy driving this book is simple but powerful: "Learn by doing." Through a series of carefully selected practical examples and interactive exercises, this book seeks to equip you with the knowledge and confidence necessary to use Bash to solve real problems. It's not just about memorizing commands and options; It's about understanding the fundamental principles that will allow you to adapt and thrive in any command line environment.

From basic file operations to automating complex tasks, each chapter builds on the previous ones, allowing you to develop your skills incrementally. Through repetition and practice, what may initially seem complex will become second nature. This practical approach ensures that, by the end of the book, you will not only be able to follow the examples presented, but also improvise your own solutions to new and unexpected problems.

Each example in the book has been selected not only for its practical relevance, but also for its ability to illustrate important concepts of Bash and shell programming in general. By breaking down each example, we will explain not only the "how" but also the "why," providing a deep understanding of the foundation behind each solution.

This book is for you if you are a student delving into the world of computing, an IT professional looking to expand your skills, or simply a technology enthusiast eager to learn how to make the most of the power of the Bash shell. Whatever your current level of experience, we invite you to dive into the examples, experiment with them, and most importantly, have fun in the process.

Let's embark on this learning adventure together, exploring the vast and powerful world of Bash, and discover how, through practice and experimentation, we can unlock new skills and open up new possibilities. Welcome to "Bash through Examples: Learning by Doing." It's time to write, run and learn!

# Task script

To provide a complete example with statement and solution in a Bash script, I will first define a simple problem and then show you how to solve it with a Bash script.

**Create a Bash script that performs the following tasks:**

1\. Check if a specific directory exists. The directory to check will be passed as an argument to the script.

2\. If the directory exists, the script should list all files and directories within it.

3\. If the directory does not exist, the script must create it.

Bash Script Solution

Next, I show you what the Bash script that solves the previous problem would look like:

bash

#!/bin/bash

# Save the first argument in a variable

directory=$1

# Check if the directory exists

if [ -d "$directorio" ]; then

echo "The directory $directory already exists. Listing contents:"

# List the contents of the directory

ls -l $directory

else

echo "The directory $directory does not exist. Creating it..."

# Create the directory

mkdir $directory

echo "Directory $directory created successfully."

be

How to Use the Script

1\. First, you must save the script to a file. For example, `check_directory.sh`.

2\. Next, you must give the file executable permissions with the command `chmod +x verify_directory.sh`.

3\. Finally, you can run the script by passing the directory name as an argument. For example: `./verify_directory.sh my_directory`.

This script is a basic example that demonstrates how to handle arguments, perform conditionals, and execute basic commands in a Bash script. It is important to note that more complex use cases may require additional checks, such as checking if the user has permissions to create a directory.

# Write a Bash script that finds and replaces a word in all `.txt` files within a given directory

The directory and words (both the search word and the replacement word) will be provided as arguments to the script.

Bash Script Solution

This script will use three arguments: the directory to search for the `.txt` files, the word to search for, and the replacement word. It will loop through all the `.txt` files in the given directory, looking for the target word and replacing it with the replacement word.

bash

#!/bin/bash

# Assign arguments to variables

directory=$1

search=$2

replace=$3

# Check if the directory exists

if [ -d "$directorio" ]; then

echo "Searching for files in $directory to replace '$find' with '$replace'..."

# Find all .txt files and perform replacement

find $directorio -type f -name "*.txt" -print0 | while IFS= read -r -d '' archivo; do

sed -i "s/$find/$replace/g" "$file"

echo "Replaced in: $file"

done

echo "Process completed."

else

echo "The directory $directory does not exist. Please check the path."

be

How to Use the Script

1\. Save the contents of the script to a file, for example, `replace_word.sh`.

2\. Give the file execute permissions with `chmod +x replace_word.sh`.

3\. Run the script with three arguments: the search directory, the word to search for, and the replacement word. For example:

./replace_word.sh ./my_directory wordSearch wordReplacement

This script is useful for making quick changes to multiple text files, especially when you need to automate text editing in a project or documents. Remember to back up your files before performing mass replacement operations, to avoid accidental data loss.

# Create a Bash script that monitors the CPU and memory usage of a specific process by name

If CPU or memory usage exceeds a specific threshold, the script should send an alert (simulated with a console message). The CPU and memory thresholds, as well as the process name, will be provided as arguments to the script.

Bash Script Solution

This script will use three arguments: the name of the process to monitor, the CPU threshold in percentage (for example, `50` for 50%), and the memory threshold in percentage. The script will periodically (every minute) check the CPU and memory usage of the process. If CPU or memory usage exceeds the set thresholds, it will print an alert to the console.

bash

#!/bin/bash

# Assigning arguments to variables

process_name=$1

umbral_cpu=$2

memory_threshold=$3

# Function to obtain and evaluate the resource usage of the process

process_monitor() {

# Get the PID of the process by name

pid=$(pgrep -f $process_name)

if [ -z "$pid" ]; then

echo "Process not found. Make sure '$process_name' is running."

exit 1

be

# Get the CPU and memory usage of the process

uso_cpu=$(ps -p $pid -o %cpu=)

use_memory=$(ps -p $pid -o %mem=)

# Compare CPU and memory usage with thresholds

cpu_excedido=$(echo "$uso_cpu > $umbral_cpu" | bc)

exceeded_memory=$(echo "$use_memory > $umbral_memory" | bc)

if [ $cpu_excedido -eq 1 ]; then

echo "Alert: CPU usage of '$process_name' is high (${cpu_usage}%)"

be

if [ $exceeded_memory -eq 1 ]; then

echo "Alert: Memory Usage of '$process_name' is high (${memory_usage}%)"

be

}

# Loop to monitor the process every minute

while true; do

process_monitor

sleep 60

done

How to Use the Script

1\. Save the content of the script in a file, for example, `process_monitor.sh`.

2\. Give execute permissions to the file with the command: `chmod +x monitor_process.sh`.

3\. Run the script providing the process name and CPU and memory thresholds. For example:

./monitor_proceso.sh firefox 10 20

This command will monitor the Firefox process, alerting if CPU usage exceeds 10% or memory usage exceeds 20%.

This script is a basic example and may need adjustments to fit your specific needs, especially on systems with multiple instances of the same process, where `pgrep` might need additional options to select the correct PID.

# Develop a Bash script to perform incremental backups of a directory

The script should save the backups to a specific directory and mark each backup with the date and time of its creation. The source and destination directories will be provided as arguments to the script. Additionally, the script should delete old backups, keeping only the 3 most recent ones.

Bash Script Solution

This Bash script will perform incremental backups of the specified directory, using `rsync` for file transfer efficiency. You will use `date` to mark each backup with a timestamp and `find` combined with `rm` to manage retention of only the 3 most recent backups.

bash

#!/bin/bash

# Assigning arguments to variables

source_addr=$1

dir_destination=$2

# Check if the directories exist

if [ ! -d "$dir_origen" ]; then

echo "The source directory does not exist."

exit 1

be

if [! -d "$dir_destino" ]; then

echo "The destination directory does not exist. Creating it..."

mkdir -p "$target_dir"

be

# Create a timestamp for the backup

timestamp=$(date +"%Y-%m-%d_%H-%M-%S")

backup_name="backup_$timestamp"

# Make the backup

rsync -a --link-dest=$destination_dir/ultimo $origin_dir/ $destination_dir/$backup_number/

# Update the 'last' symbolic link to the latest backup

ln -nsf $destination_dir/$backup_name $destination_dir/last

echo "Backup completed: $backup_name"

# Clean old backups, keeping the 3 most recent ones

(cd $destination_dir && ls -d backup_* | head -n -3 | xargs -r rm -rf)

echo "Old backups deleted, keeping the 3 most recent ones."

How to Use the Script

1\. Save the script to a file, for example `backup_incremental.sh`.

2\. Give the file executable permissions with `chmod +x backup_incremental.sh`.

3\. Run the script passing the source directory and destination directory as arguments. For example:

bash

./backup_incremental.sh /path/a/source_directory /path/a/destination_directory

This script simplifies the process of making incremental backups, which is especially useful for data that changes frequently but does not require a full backup every time. The retention strategy implemented ensures that storage space is not consumed unnecessarily.

# Develop a Bash script that checks the availability of multiple websites provided as arguments and records the status of each in a log file.

The script must make an HTTP request to each website and check if the response is successful (HTTP status code 200). For each website, the script should print to the console whether the site is up or down and log this information with a timestamp to a log file.

Bash Script Solution

This script will use `curl` to make HTTP requests to the websites provided as arguments. For each site, it will check the status code of the response and log the site status in a log file along with the current date and time.

bash

#!/bin/bash

# Log file where the states of the websites will be recorded

log_file="site_status.log"

# Verify that arguments have been provided

if [ $# -eq 0 ]; then

echo "Please provide at least one website as an argument."

exit 1

be

# Feature to check the status of a website

verify_site() {

site=$1

# Make the HTTP request and get the status code

status=$(curl -o /dev/null -s -w "%{http_code}\n" $site)

# Get the current date and time

date=$(date +"%Y-%m-%d %H:%M:%S")

if [ $state -eq 200 ]; then

echo "$date: Site $site is up." | tee -a $log_file

else

echo "$date: Site $site is down (Status: $status)." | tee -a $log_file

be

}

# Iterate over each argument provided by the script

for sitio in "$@"; do

verify_site $site

done

How to Use the Script

1\. Save the script to a file, for example, `verify_sites.sh`.

2\. Give the file execute permissions with the command: `chmod +x verify_sites.sh`.

3\. Run the script providing the websites to verify as arguments. For example:

bash

./verificar_sitios.sh https://www.google.com https://www.ejemploinexistente.com

This command will check the availability of Google and a non-existent site, printing the status of each to the console and logging these statuses in the `status_sites.log` file.

This approach is useful for monitoring website availability in a simple way and recording status changes for later review.

# Develop a Bash script that converts all image files from one format to another within a specific directory.

For example, convert all images from JPEG to PNG. The source directory and the source and destination formats will be provided as arguments to the script.

Bash Script Solution

This script will use ImageMagick's `convert` to perform image conversion. We will assume that ImageMagick is already installed on the system. The script will iterate over all the source format files in the specified directory, converting them one by one to the target format.

bash

#!/bin/bash

# Verify that sufficient arguments have been provided

if [ "$#" -ne 3 ]; then

echo "Usage: $0 directory source_format destination_format"

exit 1

be

directory=$1

source_format=$2

destination_format=$3

# Verify that the directory exists

if [ ! -d "$directorio" ]; then

echo "The specified directory does not exist."

exit 1

be

# Count and convert images

quantity=0

for image in "$directory"/*.$source_format; do

if [ -f "$imagen" ]; then

name_without_extension="${image%.*}"

convert "$image" "${name_without_extension}.${destination_format}"

echo "Converted: $image to ${name_without_extension}.${destination_format}"

((quantity++))

be

done

echo "Total images converted: $amount"

How to Use the Script

1\. Save the script to a file, for example, `convert_images.sh`.

2\. Give the file execute permissions with the command: `chmod +x convert_imagenes.sh`.

3\. Run the script providing the images directory, source format and destination format. For example:

bash

./convertir_imagenes.sh /path/a/mis_imagenes jpeg png

This command will convert all JPEG images in the `/path/a/my_images` directory to PNG format.

This script is a useful tool for bulk image conversion, especially when working with a large number of files or needing to prepare images for a specific project that requires consistent formatting.

Create a Bash script that generates a report of the sizes of files and directories within a specific directory, ordered from largest to smallest size.

The script must allow the user to specify the target directory as an argument. Additionally, you should include an option for the user to choose whether to include the details of individual files in the report or just the total size of the directories.

Bash Script Solution

This script will allow the user to specify a directory and choose whether they want a detailed report (with files) or just a summary of directory sizes. You will use `du` to calculate the sizes and `sort` to sort the results.

bash

#!/bin/bash

# Verifies that at least one argument has been supplied

if [ $# -lt 1 ]; then

echo "Usage: $0 directory [verbose]"

exit 1

be

directory=$1

mode=$2 # 'verbose' to include individual files, anything else to just directories

# Verify that the directory exists

if [ ! -d "$directorio" ]; then

echo "The specified directory does not exist."

exit 1

be

# Generate the report

if [ "$mode" = "detailed" ]; then

echo "Generating detailed report for $directory"

du -ah "$directory" | sort -rh | head -n 50

else

echo "Generating directory report for $directory"

du -sh "$directory"/* | sort -rh | head -n 50

be

echo "Report generated."

How to Use the Script

1\. Save the script to a file, for example, `reporte_sizes.sh`.

2\. Give execute permissions to the file with `chmod +xreport_sizemas.sh`.

3\. Run the script passing the target directory as an argument and optionally the word `detailed` to obtain a report that includes individual files. For example:

- For a directory-only report:

bash

./reporte_sizes.sh /path/a/my_directory

- For a detailed report including files:

bash

./reporte_sizes.sh /path/a/my_detailed directory

This script is useful for system administrators or users who need to monitor space usage in their directories, allowing you to quickly identify the biggest space consumers.

# Develop a Bash script to monitor network activity on a specific interface and log any excess data usage beyond a user-defined threshold.

The script must allow the user to specify the network interface and data threshold (in MB) as arguments. If data usage exceeds the threshold in a given period of time, this event must be recorded in a log file.

Bash Script Solution

This script will use `vnstat` to monitor network usage on the specified interface. `vnstat` is a console tool that keeps track of network usage, so it must be installed on the system for this script to work correctly. The script will check data usage at regular intervals and log any excess of the threshold to a log file.

bash

#!/bin/bash

# Verify that the necessary arguments have been provided

if [ "$#" -ne 2 ]; then

echo "Usage: $0 network_interface MB_threshold"

exit 1

be

interface=$1

threshold=$(($2*1024)) # Convert MB to KB to compare with vnstat

# Log file name

log_file="exceeded_network_usage.log"

# Feature to check data usage and log overages

verify_usage() {

# Get the total KB received and transmitted in the current month

fashion=$(vnstat -i $interface --oneline | cut -d ';' -f 3.4 | tr ';' '+' | bc);

if [ "$use" -gt "$threshold" ]; then

# Log excess usage

echo "$(date +"%Y-%m-%d %H:%M:%S"): Excessive usage on $interface - ${usage}KB exceeds ${threshold}KB threshold" >> $ log_file

echo "Alert: Excessive data usage recorded."

else

echo "Data usage is within the set limit."

be

}

# Monitor network usage every 10 minutes

while true; do

verify_usage

sleep 600

done

How to Use the Script

1\. Make sure `vnstat` is installed on your system. If it is not installed, you can install it using your distribution's package manager, for example, `sudo apt-get install vnstat` on Debian/Ubuntu.

2\. Save the script to a file, for example `monitor_red.sh`.

3\. Give the file execute permissions with `chmod +x monitor_red.sh`.

4\. Run the script providing the network interface and data threshold in MB as arguments. For example:

bash

./monitor_red.sh eth0 500

This script is useful for system administrators or users interested in keeping tabs on network usage, especially on connections with data limits or to identify unusual activity on their networks.

# Write a Bash script that generates a list of all files modified in the last 24 hours in a specified directory and its subdirectories, and sends this list by email to a specified user.

The directory to monitor and the recipient's email address will be provided as arguments to the script.

Bash Script Solution

This script will use `find` to identify files modified in the last 24 hours and `mail` to email the list. Make sure the `mail` command is configured correctly on your system to send email.

bash

#!/bin/bash

# Verify that the necessary arguments have been provided

if [ "$#" -ne 2 ]; then

echo "Usage: $0 recipient_email directory"

exit 1

be

directory=$1

recipient_email=$2

# Name of the temporary file where the list will be saved

temporary_file=$(mktemp /tmp/modified_files.XXXXXX)

# Find files modified in the last 24 hours

find $directory -type f -mtime -1 > $temporary_file

# Check if the temporary file is empty

if [ -s $archivo_temporal ]; then

# Send the list by email

mail -s "Files modified in the last 24 hours" $recipient_email < $temporary_file

echo "Email sent to $recipient_email."

else

echo "No files modified in the last 24 hours were found."

be

# Delete the temporary file

rm $temp_file

How to Use the Script

1\. Save the script to a file, for example, `send_modified_files.sh`.

2\. Give the file execute permissions with `chmod +x send_modified_files.sh`.

3\. Before running the script, make sure the system can send emails from the command line. You may need to configure `sendmail` or `postfix` and adjust the `mail` settings depending on your email provider.

4\. Run the script providing the directory to monitor and the recipient's email address as arguments. For example:

bash

./send_modified_files.sh /path/to/my_directory myemail@example.com

This script is useful for monitoring changes to important directories, such as document storage areas or web directories, allowing administrators or users to keep tabs on recently modified files.

# Create a Bash script that calculates free and used space on the file system, presenting the results in a user-readable format (for example, in GB) and emailing a summary to a system administrator.

The script arguments will be the administrator's email address.

Bash Script Solution

This script will use `df` to obtain information about disk space usage and `awk` to process this information, converting it into a readable format (GB). Finally, you will use `mail` to email this information to the system administrator.

bash

#!/bin/bash

# Verify that an email address has been provided

if [ "$#" -ne 1 ]; then

echo "Usage: $0 email_address"

exit 1

be

email_admin=$1

# Temporary file name for the report

report_file=$(mktemp /tmp/disk_space_report.XXXXXX)

# Generate report

echo "Disk space report for system $(hostname)" > $report_file

echo "Generated on $(date)" >> $report_file

echo "---------------------------------------------" >> $report_file

df -h | awk 'NR>1 {print $5 " busy on partition " $1 ", with " $4 " free."}' >> $report_file

# Send report by email

if [ -s $report_file ]; then

mail -s "Disk space report - $(date +'%Y-%m-%d %H:%M:%S')" $email_admin < $report_file

echo "Report sent to $email_admin."

else

echo "Error: Disk space report is empty."

be

# Clean

rm $report_file

How to Use the Script

1\. Save the contents of the script to a file, for example, `disk_space_report.sh`.

2\. Make sure the system is configured to send emails from the command line. This may require configuring `sendmail`, `postfix`, or any other MTA (Mail Transfer Agent) you prefer.

3\. Give the script execute permissions with `chmod +x disk_space_report.sh`.

4\. Run the script providing the system administrator's email address as an argument. For example:

bash

./informe_espacio_disco.sh admin@example.com

This script is useful for system administrators who need to stay informed about the disk space usage of the systems they manage, allowing for quick identification of potential space problems before they affect operations.

# Create a Bash script that automates the creation of user accounts on a Linux system, assigning a home directory and a default password.

The script must take the username and default password as arguments. Additionally, you should check if the user already exists on the system before attempting to create it.

Bash Script Solution

This script will use the `useradd` command to create a new user, `passwd` to assign it a password, and `grep` to check if the user already exists. Make sure you run this script as root to have the necessary permissions to add users.

bash

#!/bin/bash

# Verify that the username and password have been provided

if [ "$#" -ne 2 ]; then

echo "Usage: $0 username default_password"

exit 1

be

username=$1

password=$2

# Check if the user already exists

if id "$username" &>/dev/null; then

echo "User $username already exists on the system."

exit 1

else

# Create the user with a home directory

useradd -m "$username"

# Assign the default password (use chpasswd to avoid password echo)

echo "$username:$password" | chpasswd

echo "User $username created successfully."

be

How to Use the Script

1\. Save the contents of the script to a file, for example, `create_user.sh`.

2\. Give the file execute permissions with `chmod +x create_user.sh`.

3\. Run the script as superuser, providing the username and default password as arguments. For example:

bash

sudo ./create_user.sh new_user password123

This script simplifies user management on Linux systems, allowing system administrators and IT automators to quickly create user accounts with default settings. It is especially useful in environments where you need to create multiple user accounts efficiently.

# Develop a Bash script to find and remove duplicate files in a specific directory and its subdirectories.

The script should compare the files based on their content (SHA-256 hash) and not their names. It should inform the user about any duplicate files found and delete the copies, leaving only one instance of each file. The target directory will be provided as an argument to the script.

Bash Script Solution

This script will use the `find` command to list all files in the directory and its subdirectories, and `sha256sum` to calculate the SHA-256 hash of each file, allowing duplicates to be identified by their content. Any duplicates found will be removed, leaving only one copy of each unique file.

bash

#!/bin/bash

# Verify that a directory was given as an argument

if [ $# -ne 1 ]; then

echo "Use: $0 directory"

exit 1

be

directory=$1

# Check if the directory exists

if [ ! -d "$directorio" ]; then

echo "The specified directory does not exist."

exit 1

be

# Create a temporary file to save the hashes

tempfile=$(mktemp)

# Generate SHA-256 hashes of all files in the directory and its subdirectories

find "$directorio" -type f -exec sha256sum {} + > "$tempfile"

# Find duplicates based on the hash, ignoring the first unique file

duplicates=$(awk '{print $1}' "$tempfile" | sort | uniq -d)

if [ -z "$duplicates" ]; then

echo "No duplicate files found."

rm "$tempfile"

exit 0

be

# Process each duplicate hash

echo "$duplicates" | while read hash; do

# Find files with the same hash

grep "$hash" "$tempfile" | awk '{print $2}' | tail -n +2 | while read file; do

echo "Removing duplicate file: $file"

rm "$file"

done

done

rm "$tempfile"

echo "Process completed. Duplicate files removed."

How to Use the Script

1\. Save the script to a file, for example, `remove_duplicates.sh`.

2\. Give the file executable permissions with `chmod +x remove_duplicates.sh`.

3\. Run the script providing the target directory as an argument. For example:

./remove_duplicates.sh /path/to/my_directory

This script is useful for keeping directories organized, especially those that tend to accumulate duplicate files, such as collections of photos or documents. It is important to backup your data before running this script to avoid accidental loss of important files.

# Create a Bash script to backup a list of user-supplied directories to a tar.gz file.

The script must allow the user to specify multiple directories as arguments and an output file name for the backup file. If the backup file already exists, the script should inform the user and abort the operation to prevent accidental overwrites.

Bash Script Solution

This script combines user-specified directories into a single tar.gz file, first checking if the output file already exists to prevent data loss.

bash

#!/bin/bash

# Verify that at least two arguments have been supplied

if [ "$#" -lt 2 ]; then

echo "Use: $0 output_file.tar.gz directory1 [directory2 ...]"

exit 1

be

output_file=$1

# Remove first argument to iterate over directories only

shift

# Check if the output file already exists

if [ -f "$output_file" ]; then

echo "File $output_file already exists. Aborting to avoid overwriting."

exit 1

be

# Combine the directories into a tar.gz file

tar -czf "$output_file" "$@"

echo "Successfully backed up directories in $output_file."

How to Use the Script

1\. Save the contents of the script to a file, for example, `backup_directories.sh`.

2\. Give the file executable permissions with `chmod +x directory_backup.sh`.

3\. Run the script providing the name of the output file and the list of directories to backup. Make sure the output file does not already exist. For example:

./backup_directories.sh my_backup.tar.gz /path/a/directory1 /path/a/directory2

This script makes it easy to create compressed backups of multiple directories, being a useful tool for file management and data loss prevention. It is especially valuable for periodic backups or data preparation before making significant changes to the system or applications.

# Develop a Bash script that compresses all files modified in the last 7 days into a specific directory, creating a `.zip` file with a timestamp as its name.

This script should allow the user to specify the source directory of the files to be compressed as an argument.

Bash Script Solution

This script will search the user specified directory for all files that have been modified in the last week, compress them into a `.zip` file whose name will include the current timestamp to prevent overwrites.

bash

#!/bin/bash

# Verify that a directory was given as an argument

if [ $# -ne 1 ]; then

echo "Usage: $0 source_directory"

exit 1

be

source_directory=$1

# Check if the directory exists

if [ ! -d "$source_directory" ]; then

echo "The specified directory does not exist."

exit 1

be

# Generate zip file name with timestamp

file_name="modified_files_$(date +"%Y%m%d_%H%M%S").zip"

# Find and compress files modified in the last 7 days

find $source_directory -type f -mtime -7 -print | zip $file_name -@

echo "Files modified in the last 7 days compressed in $file_name."

How to Use the Script

1\. Save the script to a file, for example, `compress_modified.sh`.

2\. Give executable permissions to the file with `chmod +x compress_modified.sh`.

3\. Run the script providing the source directory as an argument. For example:

./compress_modified.sh /path/to/my_directory

This script is useful for performing periodic backups of recently modified files, facilitating version management and data recovery. It can also serve as part of an automated backup system or file maintenance routine.

# Create a Bash script that clears temporary and cache files for specific users on a Linux system.

The script must allow the administrator to specify a list of usernames as arguments. For each user, the script will need to delete files in common temporary directories and clear the browser cache if it exists.

Bash Script Solution

This script will iterate through the list of usernames provided as arguments, checking for the existence of temporary and browser cache directories. It will then proceed to clean up these directories to free up space and potentially improve system performance.

bash

#!/bin/bash

# Verify that usernames have been provided as arguments

if [ $# -eq 0 ]; then

echo "Usage: $0 user1 [user2 ...]"

exit 1

be

# Function to clean temporary directories and cache

clear_directories() {

user=$1

# Define the temporary and cache directories to be cleaned

temp_dirs=("/tmp" "/var/tmp")

cache_dirs=("/home/$user/.cache/mozilla" "/home/$user/.cache/chromium")

# Clear temporary directories

for dir in "${temp_dirs[@]}"; do

if [ -d "$dir" ]; then

echo "Cleaning temporary directory $dir for user $user..."

rm -rf "$dir/*"

be

done

# Clear browser cache

for dir in "${cache_dirs[@]}"; do

if [ -d "$dir" ]; then

echo "Clearing browser cache $dir for user $user..."

rm -rf "$dir/*"

be

done

}

# Iterate over each user provided as an argument

for usuario in "$@"; do

echo "Processing cleanup for user: $user"

clean_directories $user

done

echo "Cleanup completed."

How to Use the Script

1\. Save the script to a file, for example, `clean_users.sh`.

2\. Give the file execute permissions with `chmod +x clean_users.sh`.

3\. Run the script as superuser, providing the usernames as arguments. For example:

bash

sudo ./clear_users.sh user1 user2

This script is particularly useful in multi-user environments where temporary files and browser cache can accumulate and take up significant disk space. Helps keep the system clean and efficient, especially on shared systems or in educational and business environments.