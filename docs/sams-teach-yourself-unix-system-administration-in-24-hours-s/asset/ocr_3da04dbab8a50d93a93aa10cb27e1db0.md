3. There's a better way to manage lists of addresses, however, and that's to use a file inclusion alias. These look a bit peculiar, but prove tremendously helpful:

```
writers: :include:/home/taylor/writers.list
```
In this situation, any mail sent to writers will be sent to every e-mail address in the specified file. The file contents will be read on demand each time a message is sent, so if it changes between newaliases runs, the changes are seen at once.

The real advantage of the :include: notation is that your users can manage their own mailing lists without you having to touch (or let them touch!) the actual /etc/aliases file. This can significantly simplify your day-to-day system administration tasks!

4. To redirect to a file, an alias can be written as

```
archive: /private/mail/archive
```
However, most sendmail configurations now disable saving directly to files because of security issues (though what security issues are associated with writing directly to a file escapes me, unless you had something like /etc/passwd as the archive file—in which case you could e-mail a line like root::0:0::: and have an instant superuser login).

5. Another mechanism that used to be widespread in sendmail installations, but is now quite limited, is the capability to have an alias point directly to a program on the server. To address the security problems, modern sendmail installations now include a special program smrsh, the sendmail restricted shell, which is used explicitly as a safe "sandbox" for running programs that are part of an alias. The alias looks like this:

```
ps: "|/bin/ps"
```
If your installation has good error messages, an attempt to send to the ps alias will result in the following information as part of the bounced test message:

```
.... The following addresses had permanent fatal errors ....
"|/bin/ps"
(reason: service unavailable)
(expanded from: toprog)
.... Transcript of session follows ....
smrsh: ps not available for sendmail programs
554 5.0.0 "|/bin/ps"... Service unavailable
```
Notice the reference to smrsh in the second-to-last line: We thought we were specifying /bin/ps, but smrsh automatically stripped the path specification and looked in its own list of known programs for ps.

To learn more about how to configure smrsh to enable access to the popular vacation program, filter, procmail, and other sophisticated e-mail filtering programs, read the smrsh man page.