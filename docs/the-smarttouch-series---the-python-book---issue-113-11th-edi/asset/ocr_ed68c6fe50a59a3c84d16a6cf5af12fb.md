# Work with Python

**License.txt:** This file contains the licence of the distributed plug-in. The XBMG project recommends the use of the Creative Commons Attribution-ShareAlike 3.0 licence for skins, and GPL 2.0 for add-ons. However, most of the copyright licences can be used.

**Note:** For the purpose of packaging, extensions/add-ons/themes/plug-ins are the same.

# 07 Providing settings for the plug-in

Settings can be provided by the file `resources/settings.xml`. These are great for user-configurable options.

```
Partial: resources/settings.xml
```xml
<settings>
  <category label="30109">
    <setting id="filter" type="bool"
      label="30101" default="false"/>
    <setting type="sep" />
    <setting id="showAll" type="bool"
      label="30106" default="false"/>
    <setting id="showWatched"
      type="bool" label="30107"
      default="true"/>
    <setting id="showUnfinished"
      type="bool" label="30108"
      default="false"/>
    <setting type="sep" />
    <setting id="forceViewMode"
      type="bool" label="30102"
      default="true"/>
    <setting id="viewMode" type="number"
      label="30103" default="504"/>
  </category>
  <category label="30110">
    <setting id="cat_hot"
      label="30002" type="bool"
      default="true"/>
    <setting id="cat_new"
      label="30003" type="bool"
      default="true"/>
  </category>
</settings>
```

```

Here, **label** defines the language id string which will then be used to display the label. **id** defines the name which will be used for programmatic access. **type** defines the data type you want to collect; it also affects the UI which will be displayed for the element. **default** defines the default value for the setting. You should always use a default value wherever possible to provide a better user experience.

The following are a few important settings types that we can use...

+   **text:** Used for basic string inputs.
**ipaddress:** Used to collect internet addresses.
**number:** Allows you to enter a number. XBMC will also provide an on-screen numeric keyboard for the input.
**slider:** This provides an elegant way to collect integer, float and percentage values. You can get the slider setting in the following format:

```
```xml
<setting label="21223" type="slider"
  id="sideinput" default="10"
  range="1,1,10" option="int" />
```
```

In the above example we are creating a slider with min range 1, max range 10 and step as 1. In the **option** field we are stating the data type we are interested in -- we can also set option to "float" or "percent".

+   **bool:** Provides bool selection in the form of on or off.
**file:** Provides a way to input file paths. XBMC will provide a file browser to make the selection of file. If you are looking to make selection for a specific type of file you can use audio, video, image or executable instead of file.
**folder:** Provides a way to browse for a folder... **Example:**

```
```xml
<setting label="12001" type="folder"
  id="folder" source="auto"
  option="writable"/>
```
```

Here, **source** sets the start location for the folder, while **option** sets the write parameter for the application.

**sep & !sep:** sep is used to draw a horizontal line in the setting dialog; !sep is used for drawing a horizontal line with text. They do not collect any input but are there for building better user interface elements...

```
```xml
<setting label="21212" type="!sep"
/>
```
```

# 08 Language support

Language support is provided in the form of the `strings.xml` file located in `resources/languages/[language name]`. This approach is very similar to many large software projects, including Android, where static strings are never used.

```
resource/language/english/string.xml **Example:**
```xml
<?xml version="1.0" encoding="utf-8"?>
<string name="yes">yes</string>
<strings>
  <string id="30001">Add subreddit</string>
  <string id="30002">Hot</string>
  <string id="30003">New</string>
  <string id="30004">Top</string>
  <string id="30005">Controversial</string>
  <string id="30006">Hour</string>
  <string id="30007">Day</string>
  <string id="30008">Week</string>
  <string id="30009">Month</string>
  <string id="30010">Year</string>
</strings>
```

```

As you may have seen in the settings.xml example, all the labels are referring to string ids. You can have many other languages as well. Depending upon the language XBMC is running in, the correct language file will be loaded automatically.

Post XBMC Frodo (12.1), strings.xml will be deprecated. Post Frodo, XBMC will be moved to a GNU gettext-based translation system; gettext uses PO files. You can use a tool called xbmc-xml2po to convert strings.xml into equivalent PO files.

# 09 Building default.py

Since our plug-in is small, it will all be contained inside `default.py`. If you are developing a more complex add-on then you can create supporting files in the same directory. If your library depends upon third-party libraries, you have two ways to go about it. You can either place the third-party libraries into the `resources/lib` folder; or bundle the library itself into a plug-in, then add that plug-in as the dependency in the `addon.xml` file.

Our plug-in works with `reddit.tv`. This is the website from Reddit which contains trending videos shared by its readers. Videos posted on Reddit are actually sourced from YouTube, Vimeo and Dailymotion.

We will be starting off `default.py` using the following imports:

```
```python
import urllib
import urllib2
import xbmcplugin
```
```