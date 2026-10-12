Now, add a non-indented statement after the “with” code block to display the file’s new status
`print(‘File Now Closed?:’, file.closed )`

Then, re-open the file and display its contents to confirm it now contains the entire text string
`with open( ‘update.txt’, ‘r+’) as file :
    text = file.read()
    print( ‘\nString:’ , text )`

Next, add indented statements to display the current file position, then reposition and display that new position
`    print( ‘\nPosition In File Now:’, file.tell() )
    position = file.seek( 33 )
    print( ‘Position In File Now:’ , file.tell() )`

Now, add an indented statement to overwrite the text from the current file position
`    file.write( ‘All Lands’ )`

Then, add indented statements to reposition in the file once more and overwrite the text from the new position
`    file.seek( 59 )
    file.write( ‘the tombstone of Karl Marx.’ )`

Finally, add indented statements to return to the start of the file and display its entire updated contents
`    file.seek( 0 )
    text = file.read()
    print( ‘\nString:’ , text )`

Save the file to your scripts directory, then open a Command Prompt window there and run this program – to see the file strings get updated