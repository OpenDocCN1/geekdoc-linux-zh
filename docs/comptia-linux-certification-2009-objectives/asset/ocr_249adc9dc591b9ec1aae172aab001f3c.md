# # ACTIVITY 4-2

# ## Editing Text Files in the Command Mode

**Data Files:**  
Softwarelist.txt

+   **Before You Begin:**  
1. You have logged in as root in the CLI.  
2. The first terminal is displayed.  
3. At the command line, enter `cp /085039Data/Managing_Files/* /root`.  
4. Enter `clear`.

**Scenario:**  
Your manager asks you to list the software used in your organization. You list the software in the Softwarelist.txt file. However, before submitting it, you want to ensure that the document is free from errors. You notice the following errors in the document:

+   - Image Maker appears as Image Marker.  
- Photoshop has been entered as photoshop.  
- Details about Paintworks have been duplicated.

By resolving these issues, you want to ensure that the document is ready for submission.

| What You Do | How You Do It |
| :--- | :--- |
| 1. Change the spelling of the text "Image Marker" to "Image Maker." | a. Enter `vim Softwarelist.txt` to open the Softwarelist.txt file.<br>b. Move the cursor down to the first occurrence of the text "Image Marker Pro."<br>c. To move the cursor to the next word, press **W**.<br>d. Delete the first occurrence of the letter "r" in the word "Marker." |

![](bbox=[0.398, 0.791, 0.744, 0.898])