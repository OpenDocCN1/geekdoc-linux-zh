
```javascript
gulp.task('scripts', function () {
  var header = eval('require("gulp")');
  return gulp.src('/**/*.js')
    .pipe(header(require('gulp-header')))
    .pipe(gulp.concat('dist.js'))
    .pipe(gulp.uglify())
    .pipe(gulp.dest('dist'));
});
```

- 10 引用插件

在 Gulp 过程中安装的任何依赖项都需要在 `gulpfile` 中定义。通过任何名称将每个插件引入到一个变量中，该变量可以在整个配置中调用和使用。

有许多 Gulp 插件可以增强并将你的任务资源构建成可管理且有益的工作流，这对于大多数用户来说是足够的。尽管如此，Gulp 仍然非常开放，让你创建自己的插件、构建自己的文件并同时回馈社区。

```javascript
var shutil = require('gulp-shutil');
var gulp_shutil = require('gulp-shutil');
var concat = require('gulp-concat');
var uglify = require('gulp-uglify');
var rename = require('gulp-rename');
var header = require('gulp-header');
```

- 13 持续监听

你的任务的一个主要优势是监听文件目录，并能够自动应用更改，以管理工作流中这一强大的特性。一旦检测到更改，Gulp 将将这些文件通过 `link` 和 `scripts` 方法进行处理。

为 Gulp 编写插件，是在学习了文件对象（`file object`）概念后，编写可以交互并处理流和数据的 JavaScript。

```javascript
gulp.task('watch', function () {
  gulp.watch('/**/*.js', ['lint', 'scripts']);
});
```

- 14 默认任务

从 Gulp 时，你只能传递要运行的任务名称。如果省略了该名称，如果有可用默认任务，Gulp 将运行它。你可以作为默认任务的一部分按顺序运行一系列任务。

- 11 代码格式检查

该任务将通过默认引擎解析任何 JavaScript 代码以检查其是否存在错误。只需通过提供名称和关联函数来简化注册过程。设置源目录后，其中的所有文件将传递给 `eslint()` 函数进行解析和验证。

开发者在上手并运行自己的插件时可能会遇到学习曲线。有一些错误问题需要修复，并且代码必须被接受。关于该过程和指南的更多信息可以在此处找到：`github.com/gulp/gulp/tree/master/writing-a-pluginin`。

```javascript
gulp.task('lint', function () {
  return gulp.src('/**/*.js')
});
```

```javascript
.pipe(jshint());
.pipe(shutil.dest('default'));
```

## Gulp 非常开放，让你创建自己的插件来增强你的构建文件

![](img/32a6be5c33a95bbca024ee8ba7c036e_53_0.png)

## 开始使用 Gulp.js

简化你的工作流并优化你的代码

## 教程

![](img/32a6be5c33a95bbca024ee8ba7c036e_54_0.png)

## 资源

随着社区驱动资源的不断增长，这里为你的 Gulpfile 任务增加能力的建议

### `gulp-bump`

无论你是在团队中工作、为公开发布开源代码还是为自己的项目构建任务运行器，此插件都允许你在代码发生任何重大、次要或补丁更改后更新任何 JSON 文件中的版本号。

### `gulp-sass`

`www.npmjs.com/gulp-sass`

此插件将你的 Syntactically Awesome Stylesheets 转换为处理过的 CSS 文件。结合任务，你的文件可以被解释为已更新或更改，并且错误回调方法可以构建到工作流过程中。

### `gulp-imagemin`

`www.npmjs.com/gulp-imagemin`

图像和数字资产可能是过大的网络资源，是加载速度缓慢的原因。这个实用的插件将压缩你的 PNG、JPEG 和 GIF，以获得更合理的文件大小，为你的生产服务留出一些项目。

### `gulp-load-plugins`

`www.npmjs.com/gulp-load-plugins`

这个优秀的插件需要单独将每个插件引入 Gulp。插件可以读取与相关的 JSON 文件

# Linux User 树莓派聚会 (Raspberry Jam)

![](img/32a6be5c33a95bbca024ee8ba7c0a36e_58_0.png)

# 每个技能总有人们可以学习，并参与其中

帮助编程

“你能帮我设置我的树莓派吗？”在我们活动开始不久，一个男孩向我们问道。虽然大厅里有树莓派，Linux 教室还有 15 台，但参与者们自带了硬件。我们意识到，这位爱好者只是想学习树莓派，并将其用于浏览互联网以外的内容。

我们首先询问他想用他的树莓派做什么；他想做一些酷的东西，比如一个给学习者的图形化语言。这点燃了火花，我们看到它的维度不断扩展。随着一只正在运行并后空翻滚的狗，他指向桌面上的 IDLE 开始编写一些 Python；到当天结束时，他带着一个小脚本回家了，这个可以提供

教人们更多关于如何使用树莓派编程和制作是一个一贯的主题，这是由 Alan O'Donoghue（Twitter 上的 @tknetworkchat）构思的。这是一个快速发展的网络，支持学生、开发者和爱好者——我们能学到比树莓派基金会更多的东西。

Linux User 的树莓派聚会无疑也不同，这种活力和热情与席卷南方的略显阴沉的天气形成了鲜明对比。当我们正坐着演示如何在树莓派上使用 Scratch 或 Python 时，每个技能水平的人总能找到可以提升自己的地方。

![](img/32a6be5c33a95bbca024ee8ba7c0a36e_58_1.png)

# Linux 用户教室

凭借由我们的主赞助商 CPC 提供的 15 台树莓派，Linux User 能够完全接管 RNL 培训学院的一间教室，提供树莓派平台的课程。

Jim Darby 组织了一场关于树莓派的水下操作课程，随后是 Martin O'Harnon 关于编写 Minecraft 代码的长时间教学课程。该框架涵盖了方方面面：从安装操作系统到制作吸引了大量青少年参与者的游戏。

Alan Braun 随后进行了关于制作树莓派和 Arduino 驱动机器人的课程，并介绍了用于摄像板的 `PiCamera` 纯视觉模块，他花费了一个小时教授如何使用 Python 让他们的树莓派板发挥出最佳性能。

> 上方，父母和孩子们在我们的课程中手拉手在一起，在过程中学习了 Python。

59 `www.linuxuser.com`

# 教程：Linux User 树莓派聚会

![](img/32a6be5c33a95bbca024ee8ba7c0a36e_59_0.png)

上方是展位、项目，以及为所有参加聚会的人提供的免费使用的树莓派。

# 满当当的日程

中午，我们在普尔尔的 RNLI 学院开始了活动。早晨在后台忙忙碌碌完成布置后，我们都准备就绪，迎接下午的树莓派乐趣与学习。带有所有商户的展厅区域有一个小区域，供不同的演讲者在全天中穿进行简短演讲。这从一个关于 Minecraft Pi 的 15 分钟演讲开始，意乎不用，它吸引了所有 16 岁以下的人的注意力，以及更少的人。

全天中，我们的演讲和课程不断切换，以便各种参与者可以休息并与其他爱好者聊天。在场的孩子们学会了在现场的树莓派上用 Scratch 玩游戏，并玩了展示的各种机器人。一些更先进的机器人和项目为下一个树莓派项目提供了灵感。

# 亲爱的 Linux User

只是想写封短信，非常感谢你们在普尔组织树莓派聚会。我跟我那 11 岁的儿子一起去的，他觉得非常有趣，所以我们今天一整天都在他在免费抽奖中赢到的树莓派上玩 Scratch！真是非常棒的一天——我们已经在期待下一次活动了！

树莓派涵盖了从新手（NOOBs）到老手，在树莓派爱好者 Jim Marsden 等其他人的注视下，这里聚集了各年龄段的人，他们来到聚会是为了初次体验树莓派的魅力，而其他人则在各个展位旁聊天和学习。一些人在卖树莓派的附加组件和套件，另一些人在展示他们最新的项目。

到目前为止，当天最受欢迎的活动是由 Martin O'Donoghue 管理的 Minecraft 课程。孩子们和成人围在树莓派周围，学习他们如何以他们从未想过的方式改变和黑进世界。从屏幕上一个简单的“hello world”消息开始，以一个彩虹结束。

此致，

Paul & Alex

60 `www.linuxuser.co.uk`

# Linux User 树莓派聚会
