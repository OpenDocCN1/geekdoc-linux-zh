
### 代码片段

```javascript
if (ref) {
  var value = null;
  try {
    eval('value = ' + parts[i].value + ';');
  }
}
```

> 列表 219 - 使用 `batch.js` 的 `eval` 实例

在列表 218 中，第一个结果指向 `lib/batch.js` 文件，这看起来是开始我们调查的好地方。为了到达那里，我们需要确保 `parts` 数组的项是 `'ref'`。注意，如果没有 `ref`，我们将跳转到第 152 行，因为 `value` 变量被初始化为 `null`。

### 代码片段

```javascript
} catch (e) {
  error = e.message;
}

if (value) {
  if (value.match(/^\w+$/)) {
    path += value;
  } else {
    error = new Error('value includes illegal characters');
    break;
  }
} else {
  error = new Error('Reference not found');
  break;
}
```

> 列表 220 - `internals.dispatch` 代替执行匿名请求

重要的部分是第 194-203 行，`resultsData` 数组根据上一个请求的 HTTP 响应进行填充。最终，这将允许我们通过第 148 行的 `"ref"` 检查，并到达我们的目标第 152 行。由于 `eval` 执行字符串参数作为代码，当输入由用户控制时，这是非常不建议的。注意在这种情况下，`eval` 函数执行的是由 `parts` 数组项硬编码字符串组成的代码。这看起来是一个很有前景的线索，因此我们需要追溯代码执行路径，看看我们是否在某个时候控制了 `parts` 数组的内容。

# 攻击性安全

通过查看 `lib/batch.js` 的剩余部分，我们发现 `internals.batch` 函数在第 88 行（列表 222）被 `internal.process` 函数调用，该函数中有几个我们需要强调的相关部分。

首先，在第 85 行定义了一个名为 `callBatch` 的回调函数，并将对 `internals.batch` 函数的调用（称为 `parts`）作为第四个参数传递给 `internals.batch`。这就是我们处理控制的方式，我们需要跟踪它。

### 代码片段

```javascript
internals.process = function (request, requests, resultsData, reply) {

  var fnsParallel = [];
  var fnsSerial = [];
  var callBatch = function (pos, parts) {

    return function (callback) {
      internals.batch(request, resultsData, pos, parts, callback);
    };
  };
```

> 列表 222 - `process` 函数

然后位于第 92-101 行，填充了 `callBatch` 函数的 `fnsParallel` 和 `fnsSerial` 数组最终被传递给第 103 行的 `Async.series` 函数，它们在那里将触发 `callBatch` 函数的执行。

### 代码片段

```javascript
for (var i = 0, il = requests.length; i < il; i++) {
  var parts = requests[i];

  if (internals.hasPart(parts)) {
    fnsSerial.push(callBatch(i, parts));
  } else {
    fnsParallel.push(callBatch(i, parts));
  }
}

Async.series([
  function (callback) {
    Async.parallel(fnsParallel, callback);
  },
  function (callback) {
    Async.series(fnsSerial, callback);
  }
], function (err) {
  if (err) {
    reply(err);
  } else {
    reply(resultsData.results);
  }
});
```

> 列表 223 - `process` 函数的剩余部分

理解此逻辑最重要的部分是，第 96 和 99 行的 `callBatch` 函数使用名为 `parts` 的变量，该变量从 `requests` 数组填充，并作为第二个参数传递给 `internals.process` 函数。这正是我们需要继续跟踪的参数。

我们追踪练习的下一步是找到 `internals.process` 函数是从哪里调用的。再次，如果我们查看 `lib/batch.js` 文件，可以在第 69 行找到正在寻找的函数调用。

### 代码片段

```javascript
module.exports.config = function (settings) {

  return {
    handler: function (request, reply) {

      var resultsData = {
        results: [],
        resultsMap: []
      };

      var requests = [];
      var requestRegex = /(\?:\$(\d+)\)?([^/\\]]*))/g; // /project/$1.project/tasks, 不允许使用数组响应

      // 验证请求
      var errorMessage = null;
      var parseRequest = function ($0, $1, $2) {
        if ($1) {
          if ($1 < $i) {
            parts.push({type: 'text', index: $1, value: $2});
            return '';
          }
        } else {
          errorMessage = 'Request reference is beyond array size: ' + $1;
          return $0;
        }
      };
    }
  };
```

### 代码片段

```javascript
for (var i = 0, il = request.payload.requests.length; i < il; i++) {
  // 拆分为部分
  var parts = [];
  var result = request.payload.requests[i].replace(requestRegex, parseRequest);
  // 确保条目已处理（空）
  if (result === '') {
    requests.push(parts);
  } else {
    var errorMessage = errorMessage || 'Invalid request format at item: ' + i;
    if (errorMessage === null) {
      internals.process(request, requests, resultsData, reply);
    } else {
      reply(Boom.badRequest(errorMessage));
    }
  }
}
```

> 列表 224 - `Batch.config` 函数

我们将从头开始分析代码，看看我们如何到达 `internals.process` 调用。首先，`requestsData` 映射设置了 `requests` 和 `resultsMap` 数组（第 17 行）。随后，`requests` 变量中每个条目的 URL 路径在经过第 23 行定义的正则表达式处理后，被解析并拆分为部分（第 55 行）。这是我们需要处理的一个重要限制。

如果你不熟悉 JavaScript，这种情况的逻辑比较难以跟踪，我们将将其进一步拆解。具体来说，JavaScript 中的 `replace` 函数可以接受一个正则表达式作为第一个参数，接受一个函数作为第二个参数。在这种情况下，`replace` 函数操作的字符串（在本例中为 URL 路径）将首先通过正则表达式处理。结果是此操作返回多个参数，这些参数将作为第二个参数传递给函数。最后，函数本身执行，代码以清晰的方式进行。如果这个解释仍然让你感到困惑，我们建议你阅读 `String.prototype.replace` 的文档。

注意，`parseRequest` 函数最终负责将部分类型设置为 `"text"`，这正如我们之前描述，是到达我们的 `eval` 实例所需的。根据该逻辑，第 54 行定义的 `parts` 数组由第 32 和 41 行的 `parseRequest` 函数填充。如果我们能够控制传递给 `batch.js` 处理的路径，我们就能使用用户控制的数据到达我们的 `eval` 函数。但首先，我们需要找到列表 224 中 `module.exports.config` 函数在何处被调用。这引导我们找到了 `lib/index.js` 文件。

### 代码片段

```javascript
// 加载模块
var Hoek = require('hoek');
var Batch = require('./batch');

// 声明内部变量
var internals = {
  batchEndpoint: '/batch',
  description: 'A batch endpoint makes it easy to combine requests in a single call.',
  tags: ['bassmaster']
};

exports.register = function (pack, options, next) {
  var settings = Hoek.applyDefaults(internals, options);

  pack.route({
    method: 'POST',
    path: settings.batchEndpoint,
    config: Batch.config(settings)
  });

  next();
};
```

> 列表 225 - `lib/index.js` 中定义的 `/batch` 端

> 62 https://developer.mozilla.org/en-US/docs/Web/JavaScript/Global_Objects/String/replace#Specifying_a_function_as_parameter

列表中的代码显示 `/batch` 端通过 `batch.js` 文件中定义的 `config` 函数处理请求。这意味着向此端点的格式正确的请求最终将到达我们的 `eval` 目标！

那么我们如何为此端点创建一个格式正确的请求？幸运的是，Bassmaster 插件带有一个示例文件 `examples/batch.js`，它准确地告诉我们我们需要什么。

### 代码片段

```javascript
/*
 * 测试:
 *
 * 运行服务器并尝试如下批量请求：
 * POST /batch
 * { "requests": [{ "method": "get", "path": "/profile" }, { "method": "get", "path": "/item" }, { "method": "get", "path": "/item$1.id" }] }
 * 或者对 http://localhost:8080/request 的 get 请求将为你执行上述操作
 */

internals.requestBatch = function (request, reply) {
  internals.http.inject({
    method: 'POST',
    url: '/batch',
    payload: { "requests": [{ "method": "get", "path": "/profile" }, { "method": "get", "path": "/item" }, { "method": "get", "path": "/item$1.id" }] }
  });
  reply(res.result);
};

internals.main = function () {
  internals.http.route({
    { method: 'GET', path: '/profile', handler: internals.profile },
```
