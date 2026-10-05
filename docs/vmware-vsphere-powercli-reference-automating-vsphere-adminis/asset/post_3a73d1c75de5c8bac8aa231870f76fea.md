
# FIGURE 24.46 Adding code to a repository in Windows Explorer

![](img/62596f5acc979040608a4e5111beb7d6_915_0.png)

Open the SourceTree client and navigate to the Test01 repository. On the File Status tab notice that the Test-Function01.ps file is listed under Unstaged Files (Figure 24.47).

# FIGURE 24.47 SourceTree file status

![](img/62596f5acc979040608a4e5111beb7d6_915_1.png)

Click the check box next to the *Test-Function01.ps1* file and the file will move to the Staged Files area. Enter a commit message and select Push Changes Immediately To Origin/Master (Figure 24.48). Click the Commit button. If you haven't previously supplied credentials for your GitHub account, you may be prompted for them at this point.

Enter a commit message and click Push Changes Immediately To Origin/Master.

**Figure 24.48**

![](img/62596f5acc979040608a4e5111beb7d6_916_0.png)

## Update Code in a Repository

After code is stored in a project, it is likely that at some point the code will be updated with changes on the local system, which will need to be committed to the repository. We make changes to the *Test-Function01.ps1* file to provide an example of checking in updates.

Navigate to the File Tab in SourceTree and observe that the *Test-Function01.ps1* file is back in the Unstaged Files area and that in the code area the additional line of code added is highlighted in green (Figure 24.49).

# CHAPTER 24 · SOURCE CONTROL

### 24.49 The line of code we added is highlighted in green.

![](img/62596f5acc979040608a4e5111beb7d6_917_0.png)

Click the check box next to the Test-Function01.ps1 file and it will move to the Staged Files area. Enter a commit message and check Push Changes Immediately To Origin/Master (Figure 24.50). Click the Commit button.

### 24.50 Updating your code in a repository

![](img/62596f5acc979040608a4e5111beb7d6_917_1.png)

## Check for Changes in a Repository

Working with others on the same code project means that they will likely be making changes to code, similar to those we have just demonstrated. When working in this manner, it is important that you regularly update your local system with any changes made by other people on the project. For this example, some changes to code in your repository from another system (via another user) updated the Test-Function01.ps1 file with a code change and added a new file, Test-Function02.ps1. An advantage of using SourceTree over TortoiseSVN is that it shows on your system when there are pending changes on the repository—look for a Red notification containing the number of changes over the Pull toolbar button.

To update your local system with these changes, click the Pull button on the toolbar and then click OK (Figure 24.51).

Figure 24.51 Checking for changes in a repository

![](img/62596f5acc979040608a4e5111beb7d6_918_0.png)

> **TIP** Be mindful that when you are working on projects with multiple contributors it is possible for more than one person to update, move, or remove the same code file between committed changes of the project. See the information in the video "Merge Conflict Resolution in Git with SourceTree App" for guidance on how to deal with any conflicts that may occur: https://vimeo.com/73802696.

## Revert Changes in a Repository

Suppose you wish to go back to an earlier version of a code file. GitHub supports your need to do that. You can use the SourceTree client to make a Git revert and revert the code to a previously good version of the code. For this example, let's revert the Test-Function01.ps1 file back to the Initial version.

From the SourceTree client, navigate to the File Status tab and change the view to All Files ➤ Sorted File Status. Right-click the Test-Function01.ps1 file and select Log (Figure 24.52).

# FIGURE 24.52 Reverting changes in a repository

![](img/62596f5acc979040608a4e5111beb7d6_919_0.png)

When the Log opens, look through the different versions of this file and associated comments and changes. Right-click the version you want to revert and select Reset To Commit (Figure 24.53).

# FIGURE 24.53 Reset to Commit

![](img/62596f5acc979040608a4e5111beb7d6_920_0.png)

Click OK to confirm the reset (Figure 24.54).

# FIGURE 24.54 Click OK.

![](img/62596f5acc979040608a4e5111beb7d6_920_1.png)

You can verify that the `Test-Function01.ps1` file has reverted to the content you chose with `Write-Host`:

```
Get-Content C:\GitHub\Test01\Test-Function01.ps1
```
```powershell
function Test-Function01 {
    Write-Host "This is test 1"
}
```

This locally made change needs to be committed to the repository to make it the definitive version (for now) for everyone else. Navigate to the File Status tab, see the view back to Pending Files ➤ Sorted File Status, and verify that the `Test-Function01.ps1` file is in the Unstaged Files area (Figure 24.55).

# CHAPTER 24 · SOURCE CONTROL

# FIGURE 24.55 Verify that the Test-Function01.ps1 file is in the Unstaged Files area.

![](img/62596f5acc979040608a4e5111beb7d6_921_0.png)

Click the check box next to the Test-Function01.ps1 file and it will move to the Staged area. Enter a commit message and select Push Changes Immediately To Origin/Master. Click the Commit button (Figure 24.56).

# FIGURE 24.56 Click Commit to revert changes in a repository.

![](img/62596f5acc979040608a4e5111beb7d6_921_1.png)

## Remove Code from a Repository

Finally, in this set of repository actions, let's examine how to remove the Test-Function02.ps1 file from the repository.

Navigate to the C:\GitHub\Test01 folder and delete the Test-Function02.ps1 file. Within the SourceTree client, navigate to the File status tab and verify that the Test-Function02.ps1 file is in the Staged Files and that it is accompanied by a red icon (Figure 24.57).

Figure 24.57 Check the file status after deleting a file

![](img/62596f5acc979040608a4e5111beb7d6_922_0.png)

Click the check box next to the Test-Function02.ps1 file and it will move to the Staged Files area. Enter a commit message and select Push Changes Immediately To Origin/Master. Click the Commit button (Figure 24.58).

# FIGURE 24.58 Click Commit to remove the file from the repository.

![](img/62596f5acc979040608a4e5111beb7d6_923_0.png)

## Using PowerShell to Automate GitHub Client Operations

The SourceTree client we have using is actually executing commands for GitHub via a number of Git command-line tools that ship as part of the SourceTree client installation. You may notice these commands listed if you look at the full output when, for example, committing a change in the client. In the SourceTree client, it is possible to open a Terminal window to manage code in repositories with these tools. The Terminal window contains a number of visual enhancements, including colors, to make for a better experience. Out of this some functionality is not available in a PowerShell console. However, the PowerShell community has come to the rescue, and by using a project going the famous name posh-git, you can bring that functionality to a PowerShell console.

## Requirements

You will need the following:

- Git command-line tools preinstalled. You can get them from http://git-scm.com/download/win.
- posh-git, which is available from dahlbyk.github.io/posh-git/

## Installing Git Command-line Tools

Accept all the defaults during the downloaded installation apart from modifying the Windows PATH environment variable. Select Use Git from the command prompt instead (Figure 24.59).

**FIGURE 24.59 Installing Git command-line tools

![](img/62596f5acc979040608a4e5111beb7d6_924_0.png)

## Installing pos-git

The easiest way to install **pos-git** is via PsGet (http://psget.net), a tool for managing PowerShell modules. You can install PsGet and subsequently pos-git via the following two lines of code. Be sure to run both lines in a PowerShell session with administrative privileges:

```powershell
(New-Object Net.WebClient).DownloadString("http://psget.net/GetPsGet.ps1") | Invoke-Expression
Install-Module posh-git
```

Once it has been successfully installed, **pos-git** will automatically activate the PowerShell console in a folder with a Git repository. Helpful colors appear and the ability to Tab-complete Git commands will be active (Figure 24.60).

**FIGURE 24.60 PowerShell console with pos-git active**

```
C:\GitHub\Test (master *)> git status
(on branch master)
Your branch is up-to-date with 'origin/master'.
Untracked files:
  "git add <file>" to include in what will be committed
Test-Function03.ps1
nothing to commit untracked files present (use "git add" to track)
```
