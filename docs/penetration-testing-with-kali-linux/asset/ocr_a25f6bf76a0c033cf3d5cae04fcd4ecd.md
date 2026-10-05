# # OffSec Penetration Testing with Kali Linux

![](bbox=[0.125, 0.093, 0.712, 0.237])

Figure 5: XSS Testing

When we read back the blog entry, we get the following alert:

![](bbox=[0.125, 0.333, 0.712, 0.517])

Figure 6: XSS Testing Issue

In the course of making these Cross-Site requests, we keep a record of our actions, as shown below.

# Testing for Cross-Site Scripting

Testing Target: 192.168.1.52
Application: XSSBlog
Date Started: 31 March 2022

+   1. Navigated to the application http://192.168.1.52/XSSBlog.html
Result: Blog page displayed as expected

+   2. Entered our standard XSS test data:
You will rejoice to hear that no disaster has accompanied the commencement of an enterprise which you have regarded with such evil forbodings.<script>alert("Your computer is infected!");</script>\NI arrived here yesterday, and my first task is to assure my dear sister of my welfare and increasing confidence in the success of my undertaking.

+   3. Clicked Submit to post the blog entry.
Result: Blog entry appeared to save correctly.

+   4. Navigated to read the blog post

PWK - Copyright © 2023 OffSec Services Limited. All rights reserved. 93