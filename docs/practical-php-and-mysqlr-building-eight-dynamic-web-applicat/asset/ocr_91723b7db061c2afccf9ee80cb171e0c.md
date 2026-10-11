In previous projects, you accessed each piece of project functionality by loading different pages. For example, the New Topic page was used to add a new post to the forums project. In this project, however, the Web interface doesn’t need to change much, even when accessing different features. A calendar will always be visible, and the sidebar will always display different types of information. Therefore, there’s no need to create multiple pages. This further simplifies the application, which is never a bad thing.

To make the calendar even more dynamic, you will use an exciting technology called Ajax to prevent the need for refreshing the entire page when you want to access new functionality.

# ## All About Ajax

Ajax, which is sometimes referred to as Asynchronous JavaScript and XML, is an exciting technology that has been taking the Web development world by storm. Ajax has been largely spurred on by some innovative uses of the technology by Google with Gmail (http://mail.google.com) and Google Maps (http://maps.google.com).

The idea behind Ajax is that you can send requests to a server, as you normally do; but instead of refreshing the entire page, you use JavaScript to update only a portion of the page. As a result, Web applications aren’t constantly forcing users to wait for entirely new pages to be loaded in their browsers; the application feels more like a desktop program.

A good example of this is Google’s Gmail application. To compose a new message, you type the first few letters of the email address into a form. After you type the first few letters, a new window prompts you to select from a list of email addresses of people you have already emailed. In the background, Gmail is using Ajax to grab the list of email addresses from the server and present this list—without sending a new HTML page to the browser. Ajax offers you a fantastic way of providing a more dynamic experience for your users.

Ajax is not a singular new technology, but instead a combination of a range of technologies. These include the following:

+   - HTML
+   - CSS
+   - Document Object Model (or DOM)
+   - JavaScript
+   - XML HTTP Requests