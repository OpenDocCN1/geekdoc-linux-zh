# STORE

To store a password run **secret-tool** with the store argument. You st also specify a label for the password with the —label argument. This label will be displayed in the password manager.

Make sure to pass a unique set of attributes nas and values when storing a password. If the attributes match an already existing item, it will be updated instead of creating a new item. If invoked from a terminal or tty, then the password to store will be prompted for and only one line will be accepted.

A password to store can also be piped in via stdin. The password will be the contents of stdin until EOF. If you provide a newline via stdin it will be stored as part of the password.