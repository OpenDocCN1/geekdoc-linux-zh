# EditForm_html

The form used to view and edit the property values of an existing Book instance.

# Edit_html

The method called by EditForm_html that sets the property values of the Book instance to the new values specified on the form.

# DeleteConfirm_html

A form used to confirm the deletion of a selected Book instance.

# Delete_html

The method called by DeleteConfirm_html that actually deletes the selected Book instance.

The Books folder's contents should now look like Figure 10-10.

![](bbox=[0.176, 0.223, 0.725, 0.533])

Figure 10-10: Management screen after you create all DTML methods needed to manage your books

Congratulations! You have now established the basic framework for managing your books. The only things missing are the DTML methods necessary to allow customers to order your books.

# 10.4 Selling Your Books

To make it easy for people to order books from your site, you'll create a DTML method called index_html, plus the DTML methods OrderForm_html and Order_html, which index_html needs to complete its ordering mechanism. The index_html method looks like the DTML method admin_html, except that the visitor does not see the Edit Book and Delete Book buttons or the Last Modified field. Instead, the visitor's page contains a button called To Order Form, which opens the DTML method OrderForm_html.