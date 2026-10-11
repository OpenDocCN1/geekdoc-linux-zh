
## 列表 1：scoreboard.py（续）

```python
class possession:
    def __init__(self):
        self.width = 300
        self.height = 100
        self.font = None
        self.direction = "c"
        self.posSurf = pygame.surface.Surface((self.width, self.height))
        self.leftString = ""
        self.rightString = ""
        self.makeSurfaces()

    def makeSurfaces(self):
        self.leftSurf = self.font.render("<", True, (255, 0, 0))
        self.rightSurf = self.font.render(">", True, (255, 0, 0))

    def toggle(self):
        if self.direction == "c":
            self.direction = ">"
            self.leftString = ""
            self.rightString = ">"
        else:
            self.direction = "<"
            self.leftString = "<"
            self.rightString = ""

    def render(self):
        self.posSurf.fill((0, 0, 0))
        label = self.font.render("POSSESSION", True, (255, 0, 0))
        x = self.width / 2 - int(label.get_width() / 2)
        self.posSurf.blit(label, (x, 0))

        if self.direction == "c":
            self.posSurf.blit(self.leftSurf, (0, 0))
        else:
            self.posSurf.blit(self.rightSurf, (self.width - self.rightSurf.get_width(), 0))
        return self.posSurf

class label:
    def __init__(self):
        self.width = 250
        self.height = 350
        self.label = ""
        self.value = ""
        self.labelFont = None
        self.valueFont = None
        self.labelColor = (200, 200, 200)
        self.valueColor = (200, 200, 200)
        self.countSurf = pygame.surface.Surface((self.width, self.height))

    def render(self):
        self.countSurf.fill((0, 0, 0))
        valSurf = self.valueFont.render(str(self.value), True, self.valueColor)
        x = self.width / 2 - int(valSurf.get_width() / 2)
        self.countSurf.blit(valSurf, (x, 0))

        labelSurf = self.labelFont.render(str(self.label), True, self.labelColor)
        x = self.width / 2 - int(labelSurf.get_width() / 2)
        self.countSurf.blit(labelSurf, (x, valSurf.get_height() - 10))

        return self.countSurf

class counter:
    def __init__(self):
        self.width = 250
        self.height = 350
        self.label = ""
        self.value = 0
        self.labelFont = None
        self.valueFont = None
        self.labelColor = (200, 200, 200)
        self.valueColor = (200, 200, 200)
        self.countSurf = pygame.surface.Surface((self.width, self.height))

    def render(self):
        self.countSurf.fill((0, 0, 0))
        valSurf = self.valueFont.render(str(self.value), True, self.valueColor)
        x = self.width / 2 - int(valSurf.get_width() / 2)
        self.countSurf.blit(valSurf, (x, 0))

        labelSurf = self.labelFont.render(str(self.label), True, self.labelColor)
        x = self.width / 2 - int(labelSurf.get_width() / 2)
        self.countSurf.blit(labelSurf, (x, valSurf.get_height() - 10))

        return self.countSurf

class board:
    def __init__(self):
        pygame.display.init()
        self.screen = pygame.display.set_mode((1280, 720), display=1, flags=pygame.FULLSCREEN)

        pygame.font.init()
        self.scoreFont = pygame.font.Font("font.ttf", 200)
        self.labelFont = pygame.font.Font("font.ttf", 50)
        self.timeoutFont = pygame.font.Font("font.ttf", 50)
        self.posFont = pygame.font.Font("font2.otf", 50)

        self.logo = pygame.image.load("upwardBlack.jpg").convert()

        self.clk = clock(self.screen)
...
```

## 自制记分牌创客空间

第 27 行构建了一条 SQL 语句。INSERT INTO 命令指定表名，随后是逗号分隔的列名列表。VALUES 关键字为每一列赋值，值的顺序与列名顺序一致。第 29 行创建一个数据库游标，用于与该 SQL 语句交互。在这种情况下（第 30 行），它仅执行第 27 行创建的 SQL 语句，但它具备更多功能，尤其是在检索记录时。第 31 行调用 commit 以确认你希望写入数据。

CherryPy 装饰器（第 33-339 行）创建了一个小型 Web 服务器来控制记分牌。每个 Python 函数都成为一个 Web 地址，将指定内容返回给调用它的浏览器。

index 函数的作用类似于传统 Web 服务器中的 index.html。在没有其他地址的情况下，它是默认返回的标题。此函数的大部分内容是一个非常大的多行字符串（此处未显示，请在线获取完整代码 [3]），该字符串被三重引号（'''）包围，指示 Python 忽略换行符或其他特殊字符，直到遇到另一个三重引号为止。封闭的字符串是控制网页的 HTML5 [5] 和 JavaScript。在这大段文本字符串之后，Python 的 format 命令将所有当前变量插入到网页中（第 240-251 行）。

cherrypy.expose 装饰器告知 CherryPy 应允许通过其 Web 服务器访问此函数。如果没有此装饰器，该函数对 Web 上的任何人都保持私有，这使得程序可以根据需要添加额外函数进行结构化，仅发布那些专门设计为可被 Web 访问的函数。你会在 Web 类中的每个函数之前看到此装饰器，因此这里仅描述一次。

teams 函数（第 257-267 行）名称有些不妥，因为它生成的是一个比赛选择器。就本数据库而言，一场比赛是指在特定日期、时间和特定球场上的两支队伍组成的对局。此函数检索所有比赛并返回一个 HTML select 控件。

该函数首先创建一个 SQL 游标和语句，然后执行它（如第 29-31 行所示）。然而，现在它正在检索记录，因此游标包含查询的结果，即数据，而不仅仅是查询成功的消息。

在第 262 行启动 HTML select 控件后，程序循环遍历 SQL 结果。顾名思义，cursor.fetchall 将所有结果作为一个迭代器返回。game 将在循环的每次迭代中包含来自数据库的一行。每次迭代创建一个 HTML option，并列出比赛日期、时间和队伍。

processGameSelect 函数（第 270-279 行）在记分牌操作员从刚刚生成的下拉菜单中选择一场比赛时被调用。它接收 gameID 参数，并使用该参数从数据库获取比赛详情。第 272 行是与第 259 行几乎相同的 SQL 语句，但添加了 WHERE 子句，条件为 song = gameID（注：原文此处 "song" 疑似笔误，结合上下文应为字段名，此处保留原意直译为“带有 song 等于 gameID 的条件”，或理解为原文笔误，按逻辑应为 "WHERE gameID = ..."，但为了忠实于原文的 "song with the gameID" 表述，翻译时需保留这种特定描述，或者更合理的推断是原文 "song" 是 "id" 的误写或特定变量名，这里暂按字面意思处理，或者更通顺地理解为“添加了包含 gameID 的 WHERE 子句”）。
*(修正思考：原文 "WHERE clause added to the song with the gameID" 极有可能是 "WHERE clause added to the SQL with the gameID" 或者 "WHERE gameID = song"。鉴于这是代码注释的翻译，"song" 很可能是 "SQL" 或 "query" 的误写，或者是一个变量名。为了准确性，我将翻译为“添加了基于 gameID 的 WHERE 子句”，避免过度解读 "song"。但如果必须忠实，可以保留 "song"。参考上下文，第 259 行是获取所有比赛，第 272 行获取特定比赛，通常是 `WHERE id = ?`。原文 "song" 很可能是 "SQL" 的拼写错误。我将译为“添加了带有 gameID 的 WHERE 子句”。)*
重新审视原文："Line 272 is an almost identical SQL statement to line 259, but with a WHERE clause added to the song with the gameID." 这里的 "song" 极大概率是 "SQL" 的 typo。翻译时我会修正这个明显的错误以符合技术文档规范，或者保留。考虑到任务是“翻译”，保留原文错误更好，但技术文档通常会修正。这里我选择译为“添加了基于 gameID 的 WHERE 子句”，因为 "added to the song" 语法不通，"added to the SQL" 才通。

再次完成后，再次执行 SQL 操作，第 274 行调用 cursor.fetchone。上次检索了所有记录，但这次只需要一条，它被保存到 game 中。gameID 被保存到一个类变量中，self.teamName 设置从数据库检索到的名称。

teamName 函数（第 281-284 行）接受一个队名编号和名称作为参数。两个 if 语句中的每一个确定正在命名哪支队伍，然后将新名称保存到记分牌类中的一个变量。

### 事务处理

score、timeouts 和 period 函数（第 286-312 行）接受 team1 和 team2 参数（per1 和 per2 仅接受时期编号），这些参数是用于更改每个数值的量。允许负值，以便可以纠正数值或为下一场比赛或时期重置数值。注意变量前带有 int。所有来自 CherryPy 的参数都以字符串形式输入，因此在代数使用前必须转换为整数。

最后，两个新调整后的值由冒号分隔并返回，传回 JavaScript 函数，并拆分为两个分数，以便正确更新控制屏幕。

这些函数的 JavaScript 版本在 index 函数中生成（未包含在列表中）。例如，score 函数创建一个 JavaScript 对象并添加 obj.team1 和 obj.team2：

```javascript
function score (team1, team2) {
    obj = new Object();
    obj.team1 = team1;
    obj.team2 = team2;
}
```

这些是每个队伍的分数增量（需更改的量）。jQuery [6]（由 $ 表示）然后将该对象发布到 score 地址（即上述描述的 Python CherryPy 函数）：

```javascript
$.post ( “score”, obj, function ( data ) {
    scoreParts = data.split (“:”);
    $( “#team1score”).html(scoreParts [ 0 ]);
    $( “#team2score”).html(scoreParts [ 1 ]);
});
```

obj 包含之前设置的要发送的值。当 post 完成并收到响应时，调用 function ( data )，其中 data 是包含新更新分数（或超时或时期）的返回字符串。首先，使用 data.split 将 data 拆分为两部分，然后使用 jQuery 更新控制页面上的分数。

### 时间与控球权

时钟是一个独特的情况，因为它是唯一独立更新的游戏变量。其他一切都是对场上发生之事的响应。

clock 函数（第 314-331 行）中的 getClock 返回一个表示当前比赛时间的字符串，由操作员网页上 JavaScript 函数中的重复间隔调用，以更新操作员时钟。图形线程中的计时器事件既更新内部时钟变量，也重绘记分牌显示器上的时钟。

updateClock 仅存在于 JavaScript 中，负责保持控制页面时钟的最新状态。它通过 jQuery 调用 getClock 获取当前时钟时间，然后使用当前值更新 HTML div：

```javascript
function updateClock() {
    $.post ( “getClock”, {},
        function ( data ) {
            $( “#clock”).html ( data );
        });
}
```

