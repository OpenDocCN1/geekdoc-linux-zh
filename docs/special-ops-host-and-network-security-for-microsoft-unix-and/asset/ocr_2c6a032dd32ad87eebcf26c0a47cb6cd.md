# Securing IIS • Chapter 10

Once installed, it is important to edit the URLScan.ini file to customize for your site. See www.iissecurity.info/archive/urlscan.ini for an example urlscan.ini I use as the basis for all IIS servers I secure. The various URLScan settings are explained in the following sections.

+   **The [Options] Section** This section is where you can set many of the primary options that affect how URLScan functions. The settings are as follows:
    * **AllowVerbs** This setting determines whether the [AllowVerbs] section is used (which accepts only the listed HTTP verbs) or the [DenyVerbs] section is used (which accepts all but the listed HTTP verbs). Set this value to 1 to use the [AllowVerbs] section.
    * **UseAllowExtensions** This setting determines whether the [AllowExtensions] section is used (which accepts only the listed file extensions) or the [DenyExtensions] section is used (which accepts all the listed file extensions). Set this value to 1 to use the [AllowExtensions] section.
    * **NormalizeURLBeforeScan** If this is set to 1, URLScan does its analysis after IIS has decoded and normalized the request URL. If set to 0, URLScan will see the raw URL sent by the client. Although this setting is more secure set to 1 it means that may be vulnerable to the same encoding and directory traversal attacks as IIS.
    * **VerifyNormalization** This setting specifically addresses double encoding by decoding the URL twice, and rejecting it if the two URLs do not match.
    * **AllowHighBitCharacters** If set to 0, this setting blocks all URLs that contain characters outside the ASCII character set. Set this value to 1 if you must use non-ASCII character sets on your web site.
    * **AllowDotInPath** Because URLScan determines a file extension differently than IIS, it is sometimes possible to fool URLScan into permitting a request for a blocked file extension.
    For example, if you make a request for /default.asp/nothing.htm, IIS will interpret this as a request for default.asp, with the default.htm portion passed to the PATH_INFO variable. However, since is the default behavior for scripts and executables.

![](bbox=[0.711, 0.943, 0.931, 0.966])