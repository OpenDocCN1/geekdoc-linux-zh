# Time Windows

Once you've determined the content of the state information, you'll also want to determine the time period during which the state information (such as the session ID) is valid. Sometimes, the only way to test for this is to obtain the session ID (by logging into the application, example), waiting a period of time, then trying to continue through the application. If the session ID has become ‘stale,’ then the application should prompt you to reauthenticate. If, after six hours, the session ID is still valid, then the application may be highly susceptible to replay attacks.

# Countermeasures

The best countermeasure is to log the amount of sensitive data being passed in the state information. A guide for strong session management is shown in Table 7-7.

Another security measure that often gets overlooked is application logging. The Web application's platform should already be generating logs for the operating system and Web server. Unfortunately, these logs are grossly inadequate for identifying malicious activity or re-creating a suspect event. Many events affect the user's account and should be tracked, especially when dealing with financial applications:

+   - Profile changes Record changes to significant personal information such as phone number, address, credit card information, and e-mail address.

+   - Password changes Record any time the user's password is changed.

+   - Modify user Record any time an administrator changes someone's profile or password information. This could also be triggered when other users, such as help desk employees, update another user's information. Record the account that performed the change and the account that was changed.

+   - Add/Delete user Record any time users are added to or removed from the system.

The application should log as much detail as possible. Of course, there must be a balance between the amount of information and type. For example, basic items are the source IP address, username or other identification tokens, date, and time of the event. An additional piece of information would be the session ID to identify users impersonation attacks against the users.

It might not be a good idea to log the actual values that were changed. Logs should already be treated with a high degree of security in order to maintain their integrity, if the logs start to contain Social Security numbers, credit card numbers, and other personal information, then they could be at risk of compromise from an internal employee or a single point from which a malicious user can gain the database's most important information.