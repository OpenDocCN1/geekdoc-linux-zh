24: <Thank you for your order</p>
25: <form action=index.html>
26: <input type=submit value="Okay">
27: </form>
28: </center>
29: <dml-var standard_html_footer>

This page uses dhtml-email to email you the customer's order using information from the OrderForm_html form to fill the body of the email. One special case is the order value submitted from the following select list in OrderForm_html:

```
<td><SELECT size=20 NAME="order:list">
```

This form field differs from the rest because it has "list" at the end of it, which tells Zope to convert the value submitted from the browser into a list. In this case, this is the list of Book ids selected by the user. Because the value for order is a list, we use dmlin to iterate it (Line 12) and look up the information about the Books selected (Line 13). (The lookup is necessary because only the ids for the books are passed from the form to the Order_html method.). To retrieve the other properties of each Book, we use dmlwith with sequence-item as its argument (which contains the id of each Book ordered), _getitem of the underscore namespace variable. Using the namespace, it returns the Book instance, and dmlwith puts the instance at the top of the namespace. In the dtml-block (Lines 14–19), simple dtml-var insert the property values of each selected Book instance.

# 10.4.3 Sending the Order

To email the customer's order to you, we add a mail host to the Books folder to specify the mail server responsible for sending the email. The mail host's management screen is shown in Figure 10-13.

![](bbox=[0.218, 0.635, 0.822, 0.755])

Figure 10-13: Management screen for defining a mail host

To create a mail host for with our example, choose Mail Host from the books folder's add menu and select the id to MailHost. Enter a title to describe this object if you use it, enter the Internet name of the SMTP server you will use to deliver your mail. (If you don't know this information, check with your system administrator or check the configuration of your own email software). Then click on Add.

202 Chapter 10