# Chapter 12: FastTrack Configuration and Administration

+   - Character set: A style includes the definition of which character set is used to display documents in this directory. The character set can be identified by the browser to correctly display documents in many different languages.

+   - Document footer: A footer can be added to every document in a directory that a style applies to. A footer is defined and added automatically by the Web server when any document in this directory is sent to a browser.

+   - Error responses: A style can specify how error responses are handled for documents within a directory. Obviously, documents that are not found on the server do not use the error responses defined for a specific directory ("The Entire Server" setting is System Settings:Error Responses). Error responses for a style might define something like a message regarding user authentication required to access your client directory.

+   - Log preferences: All accesses to a certain directory can be configured by a style to meet your needs. For example, you might have accesses to a product download logged in a separate file or one division of your organization might prefer that different information be logged for their section of Web pages.

+   - Remote file manipulation: This feature allows browsers to use the PUT and DELETE features of the HTTP protocol to alter files on your web server. Many browsers don't support these features, and you probably don't want many people to altering your Web pages from their browsers. But if you want to set up these features, the remote file manipulation can be set up for a style to support it.

+   - Restrict Access: This feature of styles links to the Access Control section, where you can define which hosts and which users can access files in directories that this style is assigned to.

+   - Server parsed HTML: Server parsed HTML is another name for Server-Side Includes (SSI), which was discussed at length in Chapter 10. Turning on this feature for a style means that all HTML documents in a directory using this style will be parsed by the server before being sent to the browser. This allows SSI commands to be used, but also adds to the processing load on your Web server.

# Assign Styles

The Assign Styles page allows you to apply all the settings defined for a style to a specific document subdirectory on your Web server. None of the features that you define for a style are used by any directory on your Web server until you assign the style to the directory. Settings that you defined for the entire server will also apply to all subdirectories that don't have a style assigned to them.