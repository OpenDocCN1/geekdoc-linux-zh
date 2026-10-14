3. Enter the pwd command to display your current working directory. Because you have just logged in, this should display your home directory.

4. Create a new subdirectory named "archive" within your home directory using the command mkdir archive.

5. Change to the new subdirectory you just created by entering cd archive.

6. Create a new file named "report" using this command: touch report.

7. Enter ls -l to view a detailed file listing of the files in the archive subdirectory. Can you see the size of the report file?

8. Change the name of the report file to "oldreport" using mv report oldreport.

9. Use the ls command to verify that the file report is no longer there—it has been renamed as oldreport.

10. Copy the oldreport file, making a second copy of the file in the same directory using the cp oldreport oldreport2 command.

11. Move both of these files to your home directory using this command: mv * ..

12. Enter the pwd command to check that your current working directory is still the archive subdirectory of your home directory.

13. Use a relative path to remove one of the files from your home directory by entering rm ../oldreport.

14. List all the files in the current directory using the ls command.

15. Change back to your home directory using the cd command.

16. Because the archive subdirectory is empty, you can use the rmdir command to delete it by entering rmdir archive.

17. Use ls -l to check the contents of your home directory. You should see the oldreport2 file with a size of zero.

18. Copy the termcap configuration file (its purpose is not relevant for this project) to your home directory and give it the name of an existing file by entering cp /etc/termcap oldreport2.

19. Use the ls -l command again. What happened?

20. Delete the file by entering rm oldreport2.

# Project 1-4

In this project, you explore online documentation for a Linux command. To complete this activity you should have an installed Linux system with a valid user account. This project assumes you are working in a graphical desktop.

![](bbox=[0.03, 0.86, 0.1, 0.96])