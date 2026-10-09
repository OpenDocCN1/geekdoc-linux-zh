
## The /usr/share/doc Directory

The /usr/share/doc directory contains documents installed on the system, describing in detail certain aspects of configuring or using Linux.

### HOWTOs

HOWTO documents may be installed on your system, usually under the /usr/share/doc directory. The HTML version of the files can be displayed in any web browser, including the text-based Lynx browser. The text files can be viewed through any text editor or by using the display commands such as `cat`, `more`, or `less`. HOWTOs can be found on most systems and can also be found on the web at [http://linuxdocs.org/HOWTOs/HOWTO-INDEX/howtos.html](http://linuxdocs.org/HOWTOs/HOWTO-INDEX/howtos.html) and other sites.

HOWTOs are comprehensive documents, much like FAQs, but generally not in question-and-answer format. However, many HOWTOs contain an FAQ section at the end. There are several HOWTO formats available: plain text, PostScript, PDF, and HTML. In addition to the HOWTOs, there are a multitude of mini-HOWTOs on short, specific subjects.

### Getting Help from Info Pages

To display info pages, enter `info`, with or without options and arguments. By itself, the command `info` will display the help file on how to work with info pages. Entering `info [topic]` will display the info page for the specified topic. The command `info --help` displays a brief help description.

When the info page is displayed, any text with an asterisk (`*`) in front of it is a link. Move your cursor (using the arrow keys) to the text, and then press Enter to access the linked info page. To return to the previous document, type `U` and then type `D` to return to the top of the page. Type `Q` to return to the command prompt.

### LUGs

A good source of information for Linux users and developers is Linux User Groups, or LUGs. These can be virtual (based on the web) or there may be a group of people who meet in your neighborhood. The virtual ones sometimes take the form of a message board with a question-and-answer database.

![](img/477ccb2f05b6ba1b2d563ea74f18c197_57_0.png)

## Online Help

The Internet is the best place to get documentation for any distribution of Linux. There are dedicated websites and online forums that help Linux users with specific distributions or Linux in general. Documentation for commercial distributions is available in their respective official websites. These include the release notes of different versions and updates, the deployment guide, the installation guide, and the virtualization guide. For example, the Red Hat documentation can be accessed from the URL, [www.redhat.com/docs/manuals/enterprise](www.redhat.com/docs/manuals/enterprise).

![](img/477ccb2f05b6ba1b2d563ea74f18c197_58_0.png)

Figure 1-25: The Red Hat online documentation.

# How to Access Help in Linux

## Procedure Reference: View Linux man Pages

To view Linux man pages:

1. At the command line, enter `man [command]`, where `[command]` is the command you want to view a man page for.
2. View the list of command options available for the command.
3. Close the man page for the specified command.

## Procedure Reference: Display the man Page for a Command

To display the man page for a command:

1. Log in as a user.
2. Enter `man [section] [command]` to display the man page for a specific command under a specific section.
3. Navigate through the man pages.
   - Use the **Up Arrow** or **Down Arrow** key to navigate within a page.
   - Use **Page Up** or **Page Down** to navigate through several pages.
   - Search for some specific topic in the man pages as required.
     a. Enter `/search string` to search through the man page for the specified string.
     b. If necessary, type **n** to locate the next occurrence of the string in the man page.
4. Press **Q** to close the man page.

## Procedure Reference: Use the whatis Command

To use the whatis command:

1. Log in as a user.
2. Enter `makewhatis` to build the `whatis` help database.
3. Enter `whatis command` to display the man page sections and a short description of the specified command.
4. Enter `man [section] {command}` to view the man page for the specified command under the specified section.
5. Press Q to close the man page.

## Procedure Reference: Find the Relevant man Pages Using the apropos Command

To find the relevant man pages using the `apropos` command:

1. Log in as a user.
2. Enter `apropos keyword` to search the keyword in the `whatis` database and display the matching man page sections for the specified keyword.
3. Enter `man [section] {command}` to display the man page for a specific command under a specific section.
4. Press Q to close the man page and return to the command prompt.

## Procedure Reference: Display the Info Documents of a Command

To display the info documents of a command:

1. Log in as a user.
2. Enter `info` command to read the info documents for the specified command.
3. Navigate through the info pages.
   - Use the **Up Arrow** or **Down Arrow** key to navigate within a page.
   - Use **Page Up** or **Page Down** to navigate through several pages.
   - Type **n** or **p** to move to the next or previous page, respectively.
   - Type **s** to search for a particular string on the info pages.
   - Use the **Tab** key to go to the next link.
4. Press Q to close the info page.

## Procedure Reference: Display the Options of a Command

To display the options of a command:

1. Log in as a user.
2. Enter `command --help` to display the command syntax and a list of options.
3. Enter `command -options` to use the necessary option to execute the required task.

# ACTIVITY 1-4

## Identifying Linux Documentation Types and Uses

**Before You Begin:**

1. Press **Ctrl+Alt+F5**.
2. Type `logout` and press **Enter** to log out eric from the fifth terminal.
3. Press **Ctrl+Alt+F6**.
4. Type `logout` and press **Enter** to log out robert from the sixth terminal.
5. Press **Ctrl+Alt+F1**.

**Scenario:**

Your manager, Linda, is having trouble understanding certain commands. She knows that there are several types of support documentation available, but is unsure of how to use them. She also heard that a large part of the hidden cost involved with implementing Linux is a result of limited support. She would like you to submit a report on the different types of Linux documentation and their uses. You decide to explore the available help options.

| What You Do | How You Do It |
| :--- | :--- |
| 1. Display the manual for the `gzip` command. | a. At the command line, enter `man gzip` |
| | b. Press the **Spacebar** to continue reading through the man page. |
| | c. Press **Q** to return to the command line. |
| 2. Build the `whatis` database. | a. Enter `logout` to log out `jsmith`. |
| | b. Enter `root` to log in as **root**. |
| | c. At the password prompt, enter `p@ssw0rd` |
| | d. Enter `makewhatis` to build the `whatis` database. |
| 3. Search through the man pages for the word "zip." | a. Enter `apropos zip` |
| | b. Observe that the output lists all the instances where the keyword "zip" is found. |

The makewhatis command will take approximately 15 minutes to complete.

4. View the list of locations where the keyword is found in the man pages.
   a. At the command line, enter `whatis gzip`
   b. View the results.
   c. Enter `clear` to clear the terminal screen.

5. True or False? It is common practice to write a detailed report of exactly what is installed and changed on each Linux system in your environment.
   - **True**
   - False

6. What are the additional help options that may be installed on your Linux system?
   - a) **--help**
   - b) helpme
   - c) **HOWTO**
   - d) **Textinfo**

7. In what formats are HOWTOs available?
   - a) **PostScript**
   - b) Email
   - c) **PDF**
   - d) **HTML**

# ACTIVITY 1-5

## Getting Help Using Linux Manual Pages

**Before You Begin:**

You have logged in as root in the CLI terminal.

**Scenario:**

Your organization supports customers around the world and you may have to support different customers with varying time zones. To achieve this, your system time should correspond to the time on the clients’ systems. You are unsure about the procedure to change the system date and time. You decide to browse the manual pages to find more help.

| What You Do | How You Do It |
| :--- | :--- |
| 1. Find the man page for the *date* command. | a. Enter **whatis date** to see the relevant man pages for the *date* command with various sections. |
| | b. Enter **man 1 date** to see the man page of the *date* command under section 1. |
| 2. Search through the man page. | a. Enter **/FORMAT** to move to the first instance of the text "FORMAT." |
| | b. Enter **n** to navigate to the next instance of the text "FORMAT." |
| | c. Enter **/to** view the different formats allowed for the *date* command. |
| | d. Press **Q** to close the *date* man page. |
