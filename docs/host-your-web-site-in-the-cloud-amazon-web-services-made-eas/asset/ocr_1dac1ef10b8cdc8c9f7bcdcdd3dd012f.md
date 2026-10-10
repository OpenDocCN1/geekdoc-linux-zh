The Google Chart API includes many advanced formatting and labeling options, but I kept this example fairly minimal so as to leave room for you to improve it.

The final step is to store the URL in the $ChartImages array:

```
chapter_07/statistics_chart_page.php (excerpt)

$ChartImages[] = $ChartURL;
```

The final step, after the URLs of all the charts have been saved, is to include our HTML template and then exit:

```
chapter_07/statistics_chart_page.php (excerpt)

$output_title = 'Chapter 7 Sample - Charts of CloudWatch ' .
        'Statistics';
$output_message = "Charts of CloudWatch Statistics from ${start} " .
        " to ${end}";

include 'include/statistics.html.php';
```

Finally, here's the simple HTML template for our page:

```
chapter_07/statistics_chart_page.php (excerpt)

<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Strict//EN"
        "http://www.w3.org/TR/xhtml1/DTD/xhtml1-strict.dtd">
<html xmlns="http://www.w3.org/1999/xhtml" xml:lang="en" lang="en">
<head>
        <title><?php echo $output_title ?></title>
</head>
<body>
        <h1><?php echo $output_title ?></h1>
<p><?php echo $output_message ?></p>
<?php foreach($ChartImages as $image): ?>
        <img src="<?php echo $image ?>"/>
<?php endforeach ?>
</body>
</html>
```

The important point to realize is that this program never does any actual drawing. Instead, it creates an HTML page that asks Google to do the work. When the browser renders the page it will make a call to the Google Chart API for each chart on the