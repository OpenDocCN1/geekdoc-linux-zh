| https://github.com/dnlabss/liblul | https://github.com/idear4good/GuiLite | https://github.com/vurturn/nuklear | http://xpcda.net | http://cegui.org.uk |
| --- | --- | --- | --- | --- |

Of course, you can develop your own version of the .NET core wrapper for the most adaped library, but writing a wrapper for using these libraries is a large amount of work and often represent a project by itself.

Nevertheless, some of these libraries (the most popular and largely used) have already a wrapper for NET Core developed. The library you have selected have already several versions of wrappers made by experienced individual or developer’s community who want to have access to a lightweight C graphic user interface framework (for performances as well) for their .NET Core developments.

For the following examples we have chosen to use LibUi. First because LibUi is a recognized by professional efficient library and because several implementations of a wrapper for the use with .NET Core are already developed and available, avoiding the tedious and time-consuming task of the development of our own wrapper. Moreover, it uses native widgets for each platform we intend to develop for.

# 8.4.1 Presentation of LibUI

LibUI is a simple and portable GUI library in C that uses native GUI widget on each platform it supports. This is an Opensource and free to use framework developed by a vibrant community, you can