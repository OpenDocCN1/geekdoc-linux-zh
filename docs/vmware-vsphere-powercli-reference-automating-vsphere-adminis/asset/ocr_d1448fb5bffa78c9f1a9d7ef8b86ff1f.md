Source Path / URL Enter the HTTPS clone URL from the website of the GitHub repository. (Look in the bottom-right corner of your website's homepage for a Copy To Clipboard button.) For our example, it is https://github.com/jonathanmed/Test01.git.

Destination Path Select a folder on the local system-we chose C:\GitHub\Test01.

Name We chose Test01.

Click Clone to. If you haven't previously supplied credentials for your GitHub account, you may be prompted for them at this point.

FIGURE 24.45 Adding a repository in SourceTree

![](bbox=[0.31, 0.345, 0.839, 0.545])

# # Add Code to a Repository

Now that you have a GitHub repository and its clone in a local folder, you are in a position to add some code. Let's create a function and save it in the Test-Function01.ps1 file in the folder C:\GitHub\Test01. It doesn't matter for the time being what actual in the code, but we used the following:

```
function Test-Function01 {
    Write-Host "This is test 01"
}
```

In Windows Explorer, navigate to the C:\GitHub\Test01 folder and verify that the Test-Function01.ps1 file, as well as the README.md file that was already part of the repository and a hidden GIT folder that contains Git configuration information, are all contained in the folder (Figure 24.46).