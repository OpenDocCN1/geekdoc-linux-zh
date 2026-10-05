# Listing 121 - Inspecting Visitor Record Creation Function

This PHP function is responsible for parsing various HTTP request headers, including the User-Agent, which is saved in the useragent record value.

Next, when a WordPress administrator loads the Visitor, the function will execute the following portion of code from `start.php`:

```
$count=count(VST_records($date_start, $date_finish));
foreach(VST_records($date_start, $date_finish) as $record) {
    echo '<tr class="active">
        <td scope="row">'.$date->i.'</td>
        <td scope="row">'.$date_format(date($record->datetime,$format)).'</td>
        get_option("links_updated",$record->path).'</td>
        <td scope="row">'.$record->id.'</td><a href="https://www.google.com/search?ip='.$record->ip.'#ip">'.$record->ip.'</a></td>
        <td>'.$record->user-agent.'</td>
    </tr>
    ';
    $i--;
}
```

From the above code, we'll notice that the useragent record value is retrieved from the database and inserted plainly in the Table Data (td) HTML tag, without any sort of data sanitization.

As the User-Agent header is under control, we could craft an XSS attack by inserting a script tag invoking the alert() method to generate a pop-up message. Given the immediate visual impact, this is very commonly used to verify that an application is vulnerable to XSS.

> Although we just performed a white-box testing approach, we could have discovered the same vulnerability by testing the plugin through black-box HTTP header fuzzing.

With Burp configured as a proxy and Intercept disabled, we can start our attack by first browsing to http://offsecwp/ using Firefox.

We'll go to Burp Proxy > HTTP History, right-click on the request, and select Send to Repeater: