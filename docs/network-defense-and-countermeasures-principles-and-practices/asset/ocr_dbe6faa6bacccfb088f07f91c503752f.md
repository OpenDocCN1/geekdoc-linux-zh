# CHAPTER 16 Introduction to Forensics

Even if the person erases his browsing history, retrieving it is still possible. Windows stores a lot of information in a file called index.dat (information such as web addresses, search queries, and recently opened files). You can download a number of tools from the Internet that enable you to retrieve and restore the index.dat file. Here are a few:

+   * www.eusing.com/Window_Washer/Index.htm
* www.aesoft.net/index.dat%20viewer/index.dat_viewer.htm
* http://download.cnet.com/Index-dat-Analyzer/3000-2144_4-10564321.htm

However, most forensics software will extract browser data for you. So, you should not need third-party utilities if you use, for example, AccessData's FTK, Guidance Software's EnCase, or PassMark Software's Forensics.

# In System Logs

Regardless of what operating system you are, the operating system has logs. Those logs can be critical in any forensic investigation and you should retrieve them.

# Windows Logs

Let's start with Windows XP/Vista/7/8/1.10. With all of versions of Windows, you find the logs by clicking the Start button in the lower-left corner of the desktop and then clicking the Control Panel. You then click on Administrative Tools and double-click the Event Viewer. The following outlines the logs you would check for. (Note that not all appear in every version of Windows).

> FYI: Logging
With all the that you have to turn the logging on; otherwise, there will be nothing in these logs.

+   * Security log: This is probably the most important log from a forensics point of view. It has both successful and unsuccessful login events.
* Application log: This log contains various events logged by applications or programs. Many applications record their errors in the application log.
* System log: This log contains events logged by Windows system components. This includes events such as driver failures. This particular log is not interesting from a forensics perspective as the other logs.
* Forwarded Events log: This log is used to store events collected from remote computers. This will only have data in it if forwarding has been configured.
* Applications and Services Logs: This log is used to store events from a single application or component rather than events that might have systemwide impact.