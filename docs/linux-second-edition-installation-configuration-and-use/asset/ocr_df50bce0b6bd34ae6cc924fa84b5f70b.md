Depending on which server or your Internet provider are using, Shift+L may not work: no groups are displayed. This is particularly likely if you use leafnode as a news server. Quit strn with Q, and use an editor to insert the following line into the configuration file ~/.strnrc:

```
set read.active 1
```

As you see the list of groups, you can subscribe to the required groups-with S, U cancels the subscription. If you now execute Shift+L a second time, only the subscribed groups are displayed.

# Usage

To read the news of a group, you select the group with the cursor keys and press -> Now strn displays a list of all articles out of which you can select the required article, again using the cursor keys and <-

In the text window appearing on screen, you can scroll with Spacebar and With H and Z view/hide the news text or the news list. Further commands can be found in the following table:

# strn keyboard shortcuts

+   - Q quit current view or strn
- ? online help
- C mark all articles as 'read' (catchup)
- Esc, U mark all articles as 'unread' (uncatchup)
- Spacebar scroll news forward
- H view/hide news text
- Z view/hide news list
- F send reply (follow up) to an article as news text to the newsgroup
- R send reply (reply) to an article as email directly to the author
- Shift+P write new article (post)

# Group list

+   - S subscribe to groups
- U cancel subscription to a group (unsubscribe)
- Shift+L display all groups or only subscribed groups