
## 22.3 Setting the Special csh Variables

The `set` command is used to assign a value to a variable.

- **Enter the set command.** For example, to set the value of the history variable, type the following:
  ```
  % set history = 100 <Return>
  ```
- **Check the setting with echo.**
  ```
  % echo $history <Return>
  ```
  This should show the value stored in history:
  100

The special csh variables `home`, `path`, `shell`, `term`, and `user` have a special relationship with their uppercase counterparts. When you change the value of the lowercase variable, the uppercase variable is changed as well. If you change the value of `term`, for example, the value of `TERM` is changed automatically to match.

## 22.4 Making Backups of the Startup Files

The first step in creating or editing `.login` or `.cshrc` is to see whether you already have such files. If so, you should prepare backup copies.

- **If necessary, go to your home directory.** Remember, the `cd` command without arguments will take you to your home directory:
  ```
  % cd <Return>
  ```
- **List all files in your home directory.** Enter the `ls -a` (“list -all”) command:
  ```
  % ls -a <Return>
  ```
  If you see files named `.login` and `.cshrc`, these were probably placed in your home directory when your account was created. You may want to consult with your instructor or system administrator before editing them.
- **Make a backup copy of the existing startup file(s).**
  ```
  % cp .login .login.BAK <Return>
  % cp .cshrc .cshrc.BAK <Return>
  ```

## 22.5 A Login Message

In this section you will create a `.login` file (or edit an existing file) to display a message on the screen every time you log in. You will use the `echo` command to do this.

- **Try out the login message.** Type:
  ```
  % echo "Your wish is my command, Oh Great One." <Return>
  ```
  The shell should respond with the appropriate message:
  Your wish is my command, Oh Great One.
- **Use your text editor to open the .login file.**
  ```
  % vi .login <Return>
  ```
- **Insert a comment showing the modification date.** Put the following line at the top of `.login`:
  ```
  # This file was last modified on [today's date].
  ```
  The `#` at the beginning of the line makes this a comment. This shows a typical use of comments, which is to tell you when the file was last edited.
- **Add the message command to the file.**
  ```
  echo "Your wish is my command, Oh Great One."
  ```
- **Write the file and quit the editor.**

## 22.6 Running the Startup File

At this point, you *could* log out and log back in again to see if your `.login` works. However, there is an easier way: Use the *source* command.

- **Run the source command on the file**. Thus, to run the commands in `.login`, type:
  ```
  % source .login <Return>
  ```
  This will cause the shell to execute the commands in `.login`, as if you had just logged in. You should see the login message:
  Your wish is my command, Oh Great One.
  The shell will display this message each time you log in, unless you change it or delete it from your `.login`.

## 22.7 Changing the Prompt Symbol

The default primary prompt symbol for csh is the percent sign (`%`). You can change the prompt symbol by changing the value of the variable *prompt*. In this section, you will try out various prompts, then edit `.login` to display one of the new prompts.

- **Change the value of the prompt variable.** Type the following line:
  ```
  % set prompt = # <Return>
  ```
  This will change your shell prompt to the pound sign:
  ```
  #
  ```
- **Try out another prompt.** You can include spaces and special characters in the prompt string if you quote it:
  ```
  # set prompt = 'Your Majesty?' <Return>
  ```
  The prompt will change to the new string:
  ```
  Your Majesty?
  ```
- **Include shell variables in your prompt.** Some users like to display the pathname of their home directory as part of their prompt. Remember, home directory's pathname is stored by the shell in a variable named `home`. Try the following command (don't type Your Majesty?—it is the prompt):
  ```
  Your Majesty? set prompt = "$home > " <Return>
  ```
  The dollar sign placed in front of `home` tells the shell to put the contents of `home` in the prompt. Now your prompt should show the absolute pathname of your home directory, followed by an arrow (`>`). For example, if the absolute pathname of your home directory were `/home/you`, the prompt would now be
  ```
  /home/you >
  ```
  Let's put this prompt into your `.login`.
- **Use the text editor to edit the startup file.** Add the following to `.login`:
  ```
  set prompt = "$home > "
  ```
- **Write to the file and quit the editor.**
- **Use the source command to run the commands in .login.**
  ```
  /home/you > source .login <Return>
  ```
  Your prompt should now consist of your home directory's pathname, followed by an arrow. Thus, if your home directory were `/home/you`, you would see your login message, then the prompt
  ```
  /home/you >
  ```

## 22.8 Setting the Terminal Type

Having to set your terminal each time you log in is a nuisance—especially if you use the same kind of terminal all of the time. You can set the terminal in your `.login` file.

- **Edit your .login to set the terminal type.** Insert the following lines, substituting your terminal’s termcap code for `vt100`:
  ```
  set term = vt100
  echo "Terminal set to $term"
  ```
- **Write and quit the editor.**
- **Apply the source command to .login:**
  ```
  /home/you > source .login <Return>
  ```
  Your login message should appear, then the message:
  ```
  Terminal set to vt100
  ```

## 22.9 Making a calendar File

The calendar utility will remind you of upcoming events. This requires that you have a calendar file in your home directory and that you modify `.login` to read the calendar file.

- **Edit your .login with the text editor.** Add the following line:
  ```
  calendar
  ```
- **Write the change into the file and quit the editor.**
- **Use the text editor to create a calendar file.** Be sure to use this exact spelling of `calendar`, in lowercase letters. Otherwise, the shell won’t recognize the file.
- **Add a message to the calendar file.** Include today’s date in the message:
  ```
  This is a test for [today’s date]
  ```
- **Write the changes into the calendar file and quit the editor.**
- **Use the source command to run the .login file.**
  ```
  /home/you > source .login <Return>
  ```
  You should see your login message, the message about the terminal type, and the calendar message:
  ```
  Your wish is my command, Oh Great One.
  Terminal set to vt100
  This is a test for [today’s date]
  ```

## 22.10 Creating a .cshrc File

If you are a csh user, you may create a shell initialization file named `.cshrc`. This file is typically used for setting up command aliases and the history mechanism. In this section, you will create a one-letter alias for the history command.

- **Use the text editor to edit the .cshrc file.** Start by inserting a comment line, giving today's date:
  ```
  # This file was last modified on [today's date]
  ```
- **Use the text editor to define an alias.** Add the following line to the `.cshrc` file to create an alias for the history command:
  ```
  alias h history
  ```
- **Write the changes to the file and quit the editor.**
- **Use the source command to run the .cshrc file.**
  ```
  /home/you > source .cshrc <Return>
  ```

At this point, the alias should be set. In the next section, you will see how to use the alias to run the history command.

## 22.11 Using the history Mechanism

The history mechanism keeps a list of the commands you have used most recently, and it allows you to view and repeat commands on the list.

- **Run the history command using its alias.** Type `h` followed by Return to run the history command:
  ```
  /home/you > h <Return>
  ```
  If you correctly set up the alias for history, you should see a numbered list of the most recently executed commands. Note that the history command itself will appear as the last item on the list:
  ```
  1  set history = 100
  2  echo $history
  3  cd
  4  ls -a
  5  cp .login .login.BAK
  6  cp .cshrc .cshrc.BAK
  7  echo "Your wish is my command, Oh Great One."
  8  vi .login
  9  source .login
  10 set prompt = #
  11 set prompt = 'Your Majesty? '
  ```
