```
pro-subscribe: "`/usr/lib/mailman/mail/mailman` subscribe pro" 
pro-unsubscribe: "`/usr/lib/mailman/mail/mailman` unsubscribe pro"
```

9. Copy and paste the text just shown (starting from the line `## projectlist mailing list`) into the end of your `/etc/aliases` file.

10. Run the `newaliases` command. At this point you should be able to view the new mailing list from your Web browser. From a Web browser on the local system, type the following name in the address box:

```
http://localhost/mailman/listinfo
```

11. If everything appears to be working, begin adding more mailing lists. In my example, I created a mailing list called projectlist. The name of that project appears on the list shown in Figure 19-3.

12. Select that project name (click on it). The Info page should appear for the project.

13. Scroll to the bottom of that page and click on the project administrative interface link.

14. When prompted, type in the List Administrator Password. Now you can configure the look, feel, and behavior of your mailing list. Important information you will want to consider includes:

+   * **Privacy options** — Do you want the list to be public or private (as in, just within your organization)? Who do you want to allow to see your member list?
+   * **Send filters** — Who can post messages to the list? Is the list moderated or unmoderated? Might the list just go in one direction, for example, as a way to contact customers?
+   * **Membership management** — Can your members see other member information? What are your policies for adding and removing members?

15. When you are finished configuring the options, be sure to submit your changes.
At this point, you can allow users to join the list. Encourage them to explore and set their own user preferences.

If you encounter problems configuring mailman, refer to the `INSTALL`, `REDHAT` and `README` files in the `/usr/share/doc/mailman-*` directory.