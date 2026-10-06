# Using Linux Environment Variables

modify the PATH environment variable to add your own directories, or even the current directory symbol, to make your programs easier.

You can also create your global and local environment variables for your own use. Once you create an environment variable, it's accessible for the duration of your shell session.

There are several startup files that the bash shell executes when it starts up. These startup files can contain environment variable definitions to set standard environment variables for each bash session. When you log in to the Linux system, the bash shell accesses the /etc/profile startup file, and also three local startup files for each user, $HOME/.bash_profile, $HOME/.bash_login, and $HOME/.profile. Users can customize these to include environment variables and startup scripts for their own use.

The bash shell also provides for environment variable arrays. These environment variables can contain multiple values in a single variable. You can access the values either individually by referencing an index value or as a whole by referencing the entire environment variable array.

Finally, the chapter discussed the use of command aliases. While not environment variables, command aliases behave similar to environment variables. They allow you to define an alias name for a command, along with its parameters. Instead of having to type in a long command and parameters, you can just assign it to a simple alias and use the alias at any time in your shell session.

The next chapter dives into the world of Linux file permissions. This is possibly the most difficult topic for novice Linux users. However, to write good shell scripts, you need to understand how file permissions work and be able to use them in your Linux system.