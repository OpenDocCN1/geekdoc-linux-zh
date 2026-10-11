# Overview of tiger

Tiger_Run_CRACK=Y

that directs tiger to run Crack.

# Example 13-2 Sample tigerrc File

```
# 'rc' file for tiger.  This file is preprocessed, and thus
# *can* *only* contain variable assignments and comments.
#
-------------------------------------------------------------
#
# Select checks to perform.  Specify 'N' (uppercase) for checks
# you don't want performed.
#
Tiger_Check_PASSWD=Y # Fast
Tiger_Check_GROUP=Y Fast
Tiger_Check_ACCOUNTS=Y# Time varies on # of users
Tiger_Check_RHOSTS=Y# Time varies on # of users
Tiger_Check_NETRC=Y# Time varies on # of users
Tiger_Check_ALIASES=Y# Fast
Tiger_Check_CRON=Y# Fast
Tiger_Check_ANONFTP=Y# Fast
Tiger_Check_EXPORTS=Y# Fast
Tiger_Check_INETD=Y# Could be faster, not bad though
Tiger_Check_KNOWN=Y# Fast
Tiger_Check_PERMS=Y# Could be faster, not bad though
Tiger_Check_SIGNATURES=Y # Several minutes
Tiger_Check_FILESYSTEM=Y# Time varies on disk space... can be hours
Tiger_Check_PATH=Y# Fast for just root... varies for all
Tiger_Check_EMBEDDED=Y# Several minutes
#
# Should messages tagged with INFO be shown?
#
Tiger_Show_INFO_Mgs=N
#
# In order for this to be effective, you should define 'CRACK' in
# a 'site' file.
Tiger_Run_CRACK=Y # First time, ages; subsequent fairly quick
#
# Line size (for formatting of output)... default is 79...
# Specifying '0' means unlimited
#
Tiger_Output_Width=79
Tiger_CRON_Output_Width=0
#
# On small memory systems, a large search depth can result in out
# of memory situations for 'sort'... :-(...
Tiger_Embed_Max_Depth=3
#
Tiger_Embed_Check_Exec_Only=Y
#
Tiger_Embed_Check_SUID=Y
#
# Note that currently, device files are never reported.
Tiger_Embed_Report_Exec_Only=Y
# Who do you allow to own system files.
```