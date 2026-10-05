# OffSec Penetration Testing with Kali Linux

![](bbox=[0.228, 0.085, 0.772, 0.335])

Figure 134: Updated "Mountain Desserts" Web Application

Figure 134 shows that in the new version of the "Mountain Desserts" app, the Admin link has been replaced by an upload form. The text explains that we can upload a picture to win a contest. The tab bar also shows an orange icon displayed in the tab bar, indicating the web application is likely running the XAMPP stack. The text explains that the company wanted to switch to Windows, so we can assume that the web application is now running on a Windows system. Let's find out if we can upload a test file instead of an image.

```
kali@kali:# echo "this is a test" > test.txt
```

Listing 156 - Create a test text file

Let's upload the test file to the upload form in the browser.

![](bbox=[0.143, 0.546, 0.857, 0.663])

# Upload worked!

File test.txt has been uploaded in the uploads directory!

Figure 135: Successful Upload of test.txt

Figure 135 shows that we successfully uploaded our test file, so we know that the upload mechanism is not limited to images only. Next, let's attempt to upload the simple-backdoor.php webshell used in the previous Learning Unit.

PWK - Copyright © 2023 OffSec Services Limited. All rights reserved. 270