The next dialog asks you to start and use the application you want to profile. Use the application in a way that you expect it to be used in production. For instance, if you are profiling a web server, access it in a way that you expect it to be accessed during normal operation. For a web browser, use it in a way you expect the users to access web content.

During this learning phase, any access to files or capabilities needed by the application is granted as well as logged in the log file /var/log/audit/audit.log. Because any access is granted, you have to make sure that no attack can happen during this phase of profile creation. AppArmor does not yet protect your application.

Once you feel you have gone through all expected uses of the application, select Scan system log for AppArmor events in the YaST AppArmor Profile Wizard dialog.

For each event you are presented with a dialog where you can decide what should happen when this event occurs in the future. The dialog offers different options, depending on the event.