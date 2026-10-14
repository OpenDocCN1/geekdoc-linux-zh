One powerful example of this is with voice control. In Chapter 5 you used Apache to trigger individual scripts when a specific web page was accessed. With this input conduit abstraction, you can extend the scope of your voice input very simply. Like SMS, you create a simple web page that picks up each request and invokes `msgsvc`. You have created `voxcontrol.php` that reads as follows:

```
```php
$cmd = $HTTP_GET_VARS['cmd'];
$auth = $HTTP_GET_VARS['auth'];

if ($auth == "") {
    $auth = "public";
}
system("/usr/local/minerva/bin/msgsvc vox $auth $cmd &");
?>
```
```

This causes any existing command script called `$cmd` present in `/usr/local/minerva/etc/msg/vox/cmd` to be executed and includes typical commands to control the lights (`lights:on`, `lightsoff`), audio mixer (mute, quiet, next), and status reports (such as time and status).

Also, you know that any text written to the output is returned by the same conduit. Because this uses the vox voice input conduit, the output will be via the voice output conduit (Festival through say). You can therefore persuade the computer to enact simplistic conversations by creating scripts such as hello:

```
```sh
# /usr/local/minerva/etc/msg/vox/cmd/hello
echo Hello
```
```

and time:

```
```sh
# /usr/local/minerva/etc/msg/vox/cmd/time
$MINBASE=/usr/local/minerva

$MINBASE/bin/hdate
$MINBASE/bin/htime
```
```

# TODO: Building a Conduit

Although there are many necessary small files and directories in the creation of a conduit, the process has been made simpler by a short script that generates them all automatically, so you need only to call the following:

```
```sh
msgconduit create todo
```
```

You should see the extra directories created:

```
```text
$MINBASE/etc/msg/todo/addr
$MINBASE/etc/msg/todo/auth
$MINBASE/etc/msg/todo/cmd
$MINBASE/etc/msg/todo/xmit
```
```