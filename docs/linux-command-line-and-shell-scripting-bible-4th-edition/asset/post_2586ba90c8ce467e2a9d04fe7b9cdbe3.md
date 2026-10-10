
the field
For example, to create a form to enter employee information, you'd use

```python
dialog --form "Enter new employee" 19 50 0 \
    "Last name " 1 1 "" 1 15 30 0 \
    "First name " 3 1 "" 3 15 30 0 \
    "Address " 5 1 "" 5 15 30 0 \
    "City " 7 1 "" 7 15 30 0 \
    "State " 9 1 "" 9 15 30 0 \
    "Zip " 11 1 "" 11 15 30 0 2>data.txt
```

This code produces the form window shown in Figure 18-14.
When you enter data into the form fields and click the OK button, the form sends the data to the data.txt file. The data.txt file places each data item in order on a separate line in the file:

```
$ cat data.txt
Test
Ima
123 Main Street
Chicago
Illinois
60601
$
```

![](img/a5025f22e05b92f409563a958cac7312_683_0.png)

**FIGURE 18-14** The dialog form feature

Your script can then retrieve the form data from the file by reading the file line by line. The **head** and **tail** commands are an easy way to retrieve specific lines in the file:

```
last=$(cat data.txt | head -1)
first=$(cat data.txt | head -2 | tail -1)
address=$(cat data.txt | head -3 | tail -1)
city=$(cat data.txt | head -4 | tail -1)
state=$(cat data.txt | head -5 | tail -1)
zip=$(cat data.txt | tail -1)
```

Now you have all of the data from the form stored in variables that you can use anywhere in your script:

```
record="INSERT INTO employees (last, first, address, city, state, zip) VALUES ('$last', '$first', '$address', '$city', '$state', '$zip');"
echo $record>> newrecords.txt
```

The newrecords.txt file will contain the **INSERT** statements for each new form record so that you can easily import them all into a database.

You can then create a simple front-end menu for the scripts and put everything together:

```bash
#!/bin/bash
temp=$(mktemp -t record.XXXX)

function newrecord {
  dialog --form "Enter new employee" 19 50 0 \
"Last name " 1 1 "" 1 15 30 0 \
"First name " 3 1 "" 3 15 30 0 \
"Address " 5 1 "" 5 15 30 0 \
"City " 7 1 "" 7 15 30 0 \
"State " 9 1 "" 9 15 30 0 \
"Zip " 11 1 "" 11 15 30 0 2>$temp

last=$(cat $temp | head -1)
first=$(cat $temp | head -2 | tail -1)
address=$(cat $temp | head -3 | tail -1)
city=$(cat $temp | head -4 | tail -1)
state=$(cat $temp | head -5 | tail -1)
zip=$(cat $temp | head -6 | tail -1)
record="INSERT INTO employees (last, first, address, city,
state, zip) VALUES
('$last', '$first', '$address', '$city', '$state', '$zip');"
echo $record>> newrecords.txt
}

function listrecords {
  dialog --title "New Data" --textbox data.txt 20 50
}

while [ 1 ]
do
dialog --menu "Employee Data" 20 30 5 \
"1 "Enter new employee" \
2 "Display records" \
"3 "Exit" 2>$temp

if [ $? -eq 1 ]
then
break
fi

selection=$(cat $temp)

case $selection in
1)
newrecord ;;
2) listrecords ;;
3) break ;;
*) dialog --msgbox "Invalid selection" 10 30
esac
done
rm -f $temp 2> /dev/null
```

This script creates a simple graphical front end that allows you to quickly enter employee data to create an SQL file that you can easily import into a database.

## Summary

Interactive shell scripts have a reputation for being dull and boring. You can change that by using a few techniques and tools available on most Linux systems. First, you can create menu systems for your interactive scripts by using the case command and shell script functions.

The menu command allows you to paint a menu, using the standard echo command, and read a response from the user, using the read command. The case command then selects the appropriate shell script function based on the value entered.

The dialog program provides several prebuilt text widgets for creating Windows-like objects on a text-based terminal emulator. You can create dialogs for displaying text, entering text, and choosing files and dates by using the dialog program. Doing so brings even more life to your shell script.

If you're running your shell scripts in a graphical X Windows environment, you can utilize even more tools in your interactive scripts. For the KDE desktop, there's the kdialog program. This program provides simple commands to create window widgets for all the basic window functions. For the GNOME desktop, there are the gdialog and zenity programs. Each of these programs provides window widgets that blend into the GNOME desktop just like a real Windows application.

The next chapter dives into the subject of editing and manipulating text data files. Often the biggest use of shell scripts revolves around parsing and displaying data in text files such as log and error files. The Linux environment includes two very useful tools, `sed` and `gawk`, for working with text data in your shell scripts. The next chapter introduces you to these tools and shows the basics of how to use them.

# CHAPTER 19

# Introducing sed and gawk

## IN THIS CHAPTER

- **Manipulating text**
- **Learning about the sed editor**
- **Looking at the sed editor basic commands**
- **Getting introduced to the gawk editor**
- **Exploring sed editor basics**

By far, one of the most common functions for which people use shell scripts is to work with text files. Between examining log files, reading configuration files, and handling data elements, shell scripts can help automate the mundane tasks of manipulating any type of data contained in text files. However, trying to manipulate the contents of text files using just shell script commands is somewhat awkward. If you perform any type of data manipulation in your shell scripts, you want to become familiar with the sed and gawk tools available in Linux. These tools can greatly simplify any data handling tasks you need to perform.

# Manipulating Text

Chapter 10, “Working with Editors,” demonstrated how to edit text files using different editor programs available in the Linux environment. These editors enable easy manipulation of text contained in a text file by using simple commands or clicks of the mouse.

There are times, however, when you'll find yourself wanting to manipulate text in a text file on the fly, without having to pull out a full-fledged interactive text editor. In these situations, it’s useful to have a simple command-line editor that can easily format, insert, modify, or delete text elements automatically.

The Linux system provides two common tools for doing just that. We describe in this section the two most popular command-line editors used in the Linux world, sed and gawk.

# Getting to know the sed editor

The sed editor is called a *stream editor*, as opposed to a normal interactive text editor. In an interactive text editor, such as `vim`, keyboard commands are used interactively to insert, delete, or replace text in the data. A stream editor edits a stream of data based on a set of rules supplied ahead of time.

The `sed` editor can manipulate data in a stream based on commands either entered into the command line or stored in a command text file. The `sed` editor operates as follows:

- 1. Read one data line from the input.
- 2. Match that data with the supplied editor commands.
- 3. Change data in the stream as specified in the commands.
- 4. Output the new data to `STDOUT`.

After the stream editor matches and enacts all the commands against a line of data, it reads the next line of data and repeats the process. After the stream editor processes all the lines of data in the stream, it terminates.

Because the commands are applied sequentially line by line, the `sed` editor makes only one pass through the data stream to make the edits. This feature makes the `sed` editor much faster than an interactive editor and provides the ability to make quick changes to file data.

Here’s the format for using the `sed` command:

```
sed options script file
```

The options parameter allows you to customize the behavior of the sed command and includes the options shown in Table 19.1.

# TABLE 19.1 The sed Command Options
