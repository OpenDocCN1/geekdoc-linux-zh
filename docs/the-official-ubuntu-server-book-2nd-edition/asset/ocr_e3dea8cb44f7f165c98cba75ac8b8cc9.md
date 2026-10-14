deliver messages on its own schedule, so use this command only if you really need it.

+   - **status**  
+     Returns the current Postfix status. If Postfix is running, this command also returns the PID of the master process.
+   
+   - **abort**  
+     This is a more forceful version of the stop command and immediately kills all running Postfix processes whether they are finished or not.
+   
+   - **check**  
+     This command is much like apache2ctl check. It scans the Postfix directory structure for bad file or directory permissions and warns you about and corrects any problems it finds.

In addition to the Postfix command-line tool, Postfix provides a few other tools to help administration of the service. The postfix command can be used by regular users to get information about the current mail queue. This is useful so that you can keep track of deferred messages and answer the “I sent this e-mail two hours ago and the recipient said they didn’t get it. What happened?” questions. For instance, to get a full listing of all messages currently in the queue, type

```
$ postqueue -p
```

Sometimes you want to take action on messages in the queue besides simply flushing them. Occasionally you might want to delete a message (or maybe even all messages) in the queue. The postsuper command allows a superuser to perform privileged operations on the queue. For instance, to delete a message in the queue with a queue ID of 522, you would type

```
$ sudo postsuper -d 522
```

If you actually did want to delete all messages in the queue, you can use the word ALL in uppercase instead of a particular queue ID. You might also want to put a message on hold so that Postfix keeps it in the queue but