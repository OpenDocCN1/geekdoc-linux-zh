# Mastering Web Security

11. To make this example easy, we will include just two usernames: one will be admin and the other one be Cesar. To do that, just go to Input Field next to the Add button and type plus Add, and to do the same with the word Cesar.

12. Now, let's do the with payload set #2 (password). Here, we would normally use a password dictionary, but to make this easier, let's add a few options of password manually. To do this, just add Payload set to 2, keep the Payload type field as Simple list, and then add the following for the Payload Options field: kessen, topolino, password, letmein, qwerty. The result should be as shown in the following screenshot:

![](bbox=[0.125, 0.283, 0.857, 0.738])

Payload Sets
You can define one or more payload sets. The number of payload sets depend on the attack type defined in the Positions Various payload sets are available for each payload set, and each payload type can be customized in different ways.

Payload Options [Simple list]
This payload type configures a simple list of strings that are used as payloads.

Figure 12.29 – Adding payload options (values)

13. Go back to DVWA and copy the error message that you received when you put the wrong password: Username and/or password incorrect.

14. Go back to Burp Suite and now select Options. There, we are going to use the error as a marker to identify when the password is found. To do that, to go to Grep Match and click on Clear to erase the default values, and then paste the error message and click on Add.