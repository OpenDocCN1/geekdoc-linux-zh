
## 第 28–35 行：创建新电影

使用`Ming_useSWFSersion(version 6)`函数告诉Ming你想创建一个Flash 6版本的电影（见第28行）。

在第30–33行，`dragme`创建了一个新电影，定义了电影的宽度和高度，并将背景设置为浅灰色。

接下来，`dragme`创建了一个半径为40的`circle`（第34行），并将其填充为不透明的蓝色（第35行）。

## 第 39–45 行：添加动画

在第39行，你创建了一个`sprite`（精灵）——精灵是可以在屏幕上移动的物体。第40行使用`SWFMovieClip_add()`将该形状（第34行创建的`circle`）添加到精灵的新帧中。第41行通过调用`SWFMovie_add()`为电影创建了一个新帧，该函数返回一个指向精灵显示项的句柄。

回看从第44行开始的ActionScript代码——每个函数都引用了一个名为`circle`的对象。第44行为第43行添加的显示项分配了一个名称（`circle`）；在为对象分配了名称后，你就可以在ActionScript代码中操作该对象。

- 2. 保存你的工作并关闭编辑器。
- 3. 输入`make`并按回车。

编译器开始运行。

## 第 47–48 行：编译并保存代码

第47行将从第4行开始的`action_script`代码（定义形式）编译为更紧凑的形式，并将结果添加到电影中。最后，电影被保存为名为`dragme.swf`的文件（见第48行）。

如果你看到任何错误信息，请在继续之前修正问题。

## 运行程序

编译程序后，运行`./dragme`生成一个名为`dragme.swf`的电影。你可以使用任何支持Flash 6.0或更高版本的Flash播放器打开`dragme.swf`。当电影出现时，点击并拖动蓝色圆圈。

# 416 技术 54：节省时间的 PHP 技巧

(这并不是拼写错误；XML流中将`temperature`拼成了`temperature`。)

## 使用 PHP 脚本下载并显示 XML 文件 (curl)

请注意，每条数据都被一对描述其内部数据的标签包围。例如，预报`<Cloudy>`被`<Forecast>`和`</Forecast>`标签包围——这就是XML的本质。

列表54-2显示了一个相当短的PHP脚本，它可以下载指定邮政编码（目前硬编码为`98052`）的当前天气状况并解析XML。

### 列表 54-2：使用 PHP 查找天气状况

```php
<?php

$weather = array();

$xmlData = loadWeather();

parseWeather($weather, $xmlData);

displayWeather($weather);

function loadWeather() {

$curl = "http://www.ejse.com/WeatherService/Service.asmx/GetAttributeInfo?zipCode=98052";

$curl = curl_init();

curl_setopt($curl, CURLOPT_URL, $curl);

curl_setopt($curl, CURLOPT_TRANSFER, 1);

$xmlData = curl_exec($curl);

curl_close($curl);

return $xmlData;

}

function parseWeather($weather, $data) {

$parser = xml_parser_create();

xml_set_element_handler($parser, "startTag", "endTag");

xml_set_character_data_handler($parser, "dataHandler");

xml_parse($parser, $data);

xml_parser_free($parser);

}

function startTag($parser, $tagName, $tagAttributes) {

global $tag;

$tag = $tagName;

}

function endTag($parser, $tagName) {

  global $tag;

  $tag = "";

}

function dataHandler($parser, $data) {

  global $weather, $tag;

  $weather[$tag] = $data;

}

function displayWeather($weather) {

  echo("<html>\n");

  echo("<head>\n");

  echo("<title>\n");

  echo("Current Conditions At " . $weather["LOCATION"] . "<br></></title>\n");

  echo("</head>\n");

  echo("<body>\n");

  echo("<h4>\n");

  echo("Current Weather for: " . $weather["LOCATION"] . "<br/>\n");

  echo("</h4>\n");

  echo("<TABLE CELLPADDING=\"2\" CELLACING=\"0\" ORDER='1'>\n");

  echo("<TR><td>Forecast</td>TD><TD>" . $weather["FORECAST"] . "</TD></TR>\n");

  echo("<TR><td>Temperature</TD><TD>" . $weather["TEMPERATURE"] . "</TD></TR>\n");

  echo("<TR><td>Wind</TD><TD>" . $weather["WIND"] . "</TD></TR>\n");

  echo("<TR><td>Wind Chill</TD><TD>" . $weather["FEELSLIKE"] . "</TD></TR>\n");

  echo("<TR><td>Dewpoint</TD><TD>" . $weather["DEWPOINT"] . "</TD></TR>\n");

  echo("<TR><td>Pressure</TD><TD>" . $weather["PRESSURE"] . "</TD></TR>\n");

  echo("<TR><td>UV Index</TD><TD>" . $weather["UVINDEX"] . "</TD></TR>\n");

  echo("</TABLE>\n");

  echo("</body>\n");

  echo("</html>\n");

}

?>
```
