+   9. As seen at the end of Figure 12.19, the value that we selected on the dropdown was sent as id=1, so let's play around with that number to see how we secure this web application.

+   10. Let's change the value of id from 1 to 2 on Burp Suite and then click on Forward to see what happens.

+   11. If you go back to DVWA, you will see that the dropdown is still showing User ID 1; however, the information of User ID 2 is being displayed. This means Burp Suite was able to successfully inject a new value without touching the web page, as illustrated in the following screenshot:

![](bbox=[0.147, 0.296, 0.852, 0.545])

+   12. But that was just a test. Now that we see we can inject data, let's try to do a real SQL injection. To do this, let's change the value of User ID to see what we can achieve with different values. let's go back to Burp Suite and make sure that Intercept is ON and then click on Submit on DVWA to get the data on Burp Suite.

+   13. Now, Burp Suite should display the same information as shown in Figure 12.20. Here, let's go back to the road and change the value of ID from 1 to 1 OR 1=1# and click on Forward.

+   14. As you can see in the screenshot, the web page in DVWA is now displaying the information from all five users at the same time, even when there is no option to do that. This means that we just discovered a security flaw! Here it is: