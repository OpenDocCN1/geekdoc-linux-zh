```
```text
require("footer.php");
?>
```
```

# # Affirm Some Power and Moderate Some Questions

Question moderation is open to both the site administrator and the owner of the subject to which the question was added. To make this process as simple as possible, the added questions are listed as shown in Figure 9-11.

![](bbox=[0.26, 0.33, 0.93, 0.52])

Each question has three possible options: to view the details, or to allow or deny the question.

This script has a number of different personalities. To access the different pieces of functionality, the page is passed a `func` GET variable, which is then run through a `switch` statement that has five possible outcomes:

+   *   **`main.`** This section displays the summary of the questions, as seen in Figure 9-11.
+   *   **`details.`** When the user clicks the Details link, this section is loaded and displays the details about the question.
+   *   **`allow.`** If the user clicks the Allow link, this section sets the question status to live.
+   *   **`deny.`** If the user rejects the question and clicks the Deny link, this section prompts the user—with Yes and No options—to be sure he wants to deny the question.
+   *   **`denyconf.`** If the Yes option is clicked, the question is deleted.

Create a new file called *adminmodquestions.php* and add the following code: