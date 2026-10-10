# 7.3.2 **<mx:method>** tag

An **<mx:RemoteObject>** can have multiple **<mx:method>** tags as child tags. The **<mx:method>** tag specifies the operations or methods pertaining to the remote object. The syntax for this tag is shown in *Listing 7.8* below.

```
<mx:method
    concurrency="multiple|single|last"
    name="No default, required."
    makeObjectsBindable="false|true"
    fault="No default."
    result="No default."
/>

```

*Listing 7.8* - Syntax of the **<mx:method>** tag

# 7.3.3 **<mx:arguments>** tag

An **<mx:method>** tag can have a single **<mx:arguments>** tag as child tag. This tag represents an array of objects to be sent as parameter to the remote object’s method in an order.

```
<mx:arguments></mx:arguments>

```

> Note:
> It is beyond the scope of this book to discuss the usage of remote object in Flex applications as it uses the Flex Data Services.

# 7.4 Using HTTPService

Another tool that Flex provides for accessing remote data is the **HttpService Request Object**. The flex application will send an HttpService request to access remote data. Since Flex does not directly interact with the database, a Web server will respond to the Http Service Request by querying the database and returning the results. *Figure 7.5* shows how Flex uses HttpService for communicating with the data server.