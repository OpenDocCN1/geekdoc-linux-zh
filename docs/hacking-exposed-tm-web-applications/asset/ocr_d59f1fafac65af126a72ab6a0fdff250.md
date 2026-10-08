# Chapter 11: Hacking Web Application Management

/_vti_bin/_vti_aut/author.dll?method=list+documents%3a%3e0%2e2%2e1706&service=%5name&listHiddenDocs=true&listExplorerDocs=true&listRecourse=false&listFiles=true&listFolders=true&listLinkInfo=true&listIncludeParent=true&listDerived=false&listBorders=false

By default, FP hosting access to a server is authenticated using Windows auth (NTLM over HTTP; Chapter 5), so don't get the impression that an attacker can simply walk through the front door of your server running FPSE, although any relaxation of the default security can result in this problem. If you're concerned about the security of your FP Webs (virtual roots that allow access are called), you can right-click any server in the IISAdmin tool, select All Tasks | Check Server Extensions, and you'll be prompted to “tight security as much as possible for all FrontPage webs” (as shown in Figure 11-1).
If you check the server extensions, the following tasks will be performed:

+   - Checks reads permissions
- Checks Service.cnf and Service.lock are read/write.
- Updates Postinfo.html and _vti_inf.htm.
- Verifies that _vti_pvt, _vti_log, and _vti_bin are installed, and that _vti_bin is executable.
- Determines whether virtual roots or matlab settings are correct and up to date.
- Checks that the IUSR_michename account doesn't have write access.

+   Warns you if you are running on a FAT file system, which means that you cannot supply any Web security whatsoever.

> TIP You can also use Microsoft’s UrlScan to control access to FrontPage; see “References and Further Reading” at the end of this chapter for links on how to do this.

Over the years, FP Server Extensions have garnered a bad reputation, security-wise. The most widely publicized problem was with the FrontPage 98 Server Extension

| Check Web |
| Do you want FrontPage to tighten security as much as possible for all FrontPage webs? |
| Yes | No |

Figure 11-1. Selecting maximum security over FrontPage Webs in the IISAdmin tool