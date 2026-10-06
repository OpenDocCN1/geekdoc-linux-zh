# Chapter 24 ✦ Running a Linux, Apache, MySQL, and PHP (LAMP) Server 655

Locations are configured in the form of a start tag tagging the location type and a resource location, followed by the configuration options for that location, and finishing with an end tag. This form is often called a configuration block, and looks very similar to HTML. A special type of configuration block, known as a location block, is used to override settings for specific files or directories. These blocks take the following form:

```
<location specifier>
(options to objects matching the specifier within this block)
</locationtag>
```

Different types of location tags exist and are selected based on the type of resource location that is specified. The specifier that is included in the start tag is handled based on the type of location tag. The ones you generally use and encounter are Directory, Files, and Location.

In this chapter, Location refers specifically to the third type of tag, and location refers to any of the three.

+   * Directory tags are used to specify a path based on the location on the file system. For instance, Directory refers to the root directory on the computer. Directory inherits settings from directories above them, with the most specific Directory block overriding less specific ones, regardless of the order in which they appear in the configuration files.
* Files tags are used to specify files by name. Files can be contained within Directory blocks to limit them to files under that directory. Settings within a Files block will override the ones in Directory blocks.
* Location tags are used to specify the URI used to access a file or directory. This is different from Directory in it relates to the address contained within the request and not to the real location of the file on the drive. Location tags are processed and override the settings in Directory and Files blocks.

Match versions of these tags—DirectoryMatch, FilesMatch, and LocationMatch—have the same function but can contain regular expressions in the resource specification. FilesMatch and LocationMatch blocks are processed at the same time as Files and Location, respectively, DirectoryMatch blocks are processed after Directory blocks.

Apache can also be configured to process configuration options contained within files with the name specified in the AccessFileName directive (which is generally set to .htaccess). Directives in access configuration files are applied to all objects under the directory they contain, including subdirectories and their contents. Access configuration files are processed at the same time as Directory blocks, using a similar "most specific match" order.

![](bbox=[0.115, 0.373, 0.183, 0.413])