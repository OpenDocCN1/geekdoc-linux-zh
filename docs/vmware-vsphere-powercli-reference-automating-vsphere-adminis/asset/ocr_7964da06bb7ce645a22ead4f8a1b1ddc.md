APACHE SUBVERSION 861

For completeness, look back in the C:\Code\Project01\trunk folder and verify that the Test-Function01.ps1 file now displays with an icon with a green check mark and confirm that there are no outstanding changes to the file that needs to be committed to the project (Figure 24.26).

# FIGURE 24.26 Confirm that there are no outstanding changes.

![](bbox=[0.277, 0.237, 0.843, 0.563])

# Check for Changes in a Project with TortoiseSVN

Working with other people on the same code project means that they will likely be making changes to code, too. When working in this manner, it is important that you regularly update your local system with any changes made by other people on the project. To continue with this example, use another system to connect to this project via a different user account than the one used already, and make some changes. We logged in as another user and updated with an additional Write-Host line:

```
function Test-Function01 {
    Write-Host "This is test 01"
    Write-Host "This is test 01"
    Write-Host "This is test 01"
}
```

PowerCLI and DevOpsnPART VI