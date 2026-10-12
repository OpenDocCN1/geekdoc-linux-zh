To save future headaches, execute the following command:
`cat /data/web/apache/secrets/.htpasswd`
This should show a line similar to the following (the password won't be exactly the same as this example):
`reader:hulr6FFphLsxK6`
This confirms that you have a user called reader in the .htpasswd file. The password bought-it is encrypted by the htpasswd program using the standard crypt() function.

+   2. Create an .htaccess file.

Using a text editor, add the following lines to a file named `/data/web/apache/public/htdocs/chapter12/.htaccess`:
`AuthName "IDG Readers Only"`
`AuthType Basic`
`AuthUserFile /data/web/apache/secrets/.htpasswd`
`require user reader`

The following list describes the directives in the preceding syntax:

+   * `AuthName`. Sets the realm of the authentication. This is just a label with is sent to the Web browser so that the user will be provided with some clue about what he or she is about to access. In this case, the `"IDG Readers Only"` string indicates that only IDG Books readers can access this directory.

+   * `AuthType`. Specifies the type of authentication to be used. Because only basic authentication is supported, `AuthType` is always set to `Basic`.

+   * `AuthUserFile`. Specifies the filename for the user file. The path to the user file is provided here.

+   * `require`. Specifies that a user named `reader` is allowed access to this directory.

+   3. Set file permissions.

After you create the .htaccess and .htpasswd files, it is important to make sure that only Apache can read the files. No users except the file owner and Apache should have access to these files.

+   4. Test.