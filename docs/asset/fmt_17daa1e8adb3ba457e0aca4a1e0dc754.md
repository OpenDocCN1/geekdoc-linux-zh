
JavaScript 客户端和服务器现在建立了一个持久连接。一旦建立，客户端和服务器就可以使用 WebSocket 协议向两端发送消息。它们在事件中接收消息并无延迟地处理。

为了说明这一点，我实现了一个应用程序，让我向本地服务器输入文本，然后按我的方式格式化文本，并在浏览器中以 HTML 显示结果。然而，我为“快照”专栏写文章，所以我通常以我的转换器将其转换为浏览器 HTML 的格式编写。使用 WebSocket，这意味着一旦我及时保存并调用保存，HTML 视图将立即显示消息（图 2）。

在当前情况下，WebSocket 服务器注意到本地文件系统的变化。每当用户修改文件时，服务器向客户端发送消息。该行代码随后通知 JavaScript 引擎，从服务器重新加载页面。

## 变化告警

但如果文件最近更改过呢？就像快照本地栏中的 `watch` 一样，两者使用内核的 `notify` 函数或对整个目录条目监控。

## 多任务调度板

当服务器向文件系统发送数据时，它使用 WebSocket 连接来消息。

- 快如闪电 (Linux 2025)
- POD 错误

## 快如闪电 (Linux 2025)

你可能想过，比如 WhatsApp 或 Slack 在你的浏览器中打开时，为什么能对对方“正在输入”的反馈响应如此迅速……即使在消息发送之前，浏览器至少需要响应（图 #10）做那个，至少几乎需要重新加载你正在查看的页面，但它是如何知道何时这么做的？

图 2：为“快照”专栏编写文章。

LINUX-MAXIMUM.COM 第 296 期 2025 年 7 月

## 深度解析

### 编程快照 – WebSockets

该实现是面向对象的。第 16 行的 `NewServer()` 构造函数返回一个指向 `WServer` 类型（定义的结构体）的指针，其中包含一个来自 Uber `zap` 路径的日志器和一个用于所有 WebSocket 连接的 `clients` 映射。

### 通过未检查的通过

列表 2 第 23 行开始的 `Handler()` 函数定义了客户端首次连接到 WebSocket 的时。WebSocket 使用 HTTP 协议来建立传输机制（即 WebSocket 充当某种 HTTP 升级）。

之所以这样做是因为 WebSocket 服务器处理的是客户端，而不仅仅是一个，或者同时处理多个。为了做到这一点，它为每个客户端保持一个连接，并在传入的消息之间进行多路复用。响应的情况下，所有连接的客户端都会接收带有更改文件路径的消息。通过这种方式，多个标签页可以同时连接到 WebSocket 服务器并刷新它们的显示。

第 29 行，调用 `upgrade()` 建立 WebSocket 连接，并将其作为网格存储在哈希表中。该哈希表位于对象的实例数据中，有助于将消息分发到所有已连接的客户端。

第 25 行的参数决定了升级是否应该验证传入请求的 `G` 头部。我的简单实现没有理会任何限制，只是返回 `true` 以绕过安全机制。

如数组之类的结构；它使用信号量执行此。任务诸如在哈希表中创建新条目、让它们释放或遍历哈希表中的所有条目以进行并发访问。在读取或写入此互斥锁的数据之前，Go 的 `sync` 包需要调用 `lock()` 以防止问题。在向此写入数据后调用 `unlock()`，否则很快就会导致竞态条件。

来自列表 2 的第三个函数，从第 51 行开始，向所有已连接的客户端报告已修改的文件。为了做到这一点，它遍历哈希表中的所有条目，并向客户端发送一个 JSON 消息，其中包含文件的键和路径。`json()` 函数通过将解析后的数据转换为 JSON 值对来处理格式化。

第 54 行的指令确保了当设置了 `lock()` 时，当前函数会在 `lock()` 完成前执行。忘记重置是一个好主意，特别是当你正在处理复杂的 `if` 逻辑时。

![](img/5d8ea078bd95ce53a498c7a527477ee9_59_0.png)

### JavaScript 接收器

图 4 显示了 WebSocket 连接的客户端。如果 HTML 文件头包含此 JavaScript 代码段，浏览器将调用 `new` 来向 WebSocket 服务器打开连接。

### 列表 1: innnotify.go

```go
01 package name 19 select {
02 case event, ok := <-watcher.Events
03 import 21 if ok {
04 "github.com/fsnotify/fsnotify" 22 return
05 } 23 }
06 30
07 func watchdirs(paths []string, cb func(string)) error { 24
08 watcher, err := fsnotify.NewWatcher() 25
09 if err != nil { 26
10 return err 27
11 } 28
12 29
13 if event.Op&fsnotify.Write == fsnotify.Write || fsnotify.Write == fsnotify.Create = 29
14 cb(event.Name) 30
15 31
16 for _, path := range paths { 31
17 watcher.Add(path) 32
18 } 32
19 33
20 func go() { 34
21 for { 35
22 return 36
```

60 JULY 2025 ISSUE TWO LINUX-MAGAZINE.COM

### 列表 2: websocket.go

```go
01 package main		33 }
02 import		34 	ws.ClientMutex.Lock()
03 	"github.com/gorilla/websocket"		35 	ws.Clients[conn] = true
04 	"go.uber.com/zap"		36 	ws.ClientMutex.Unlock()
05 	"net/http"		37
06 	"sync"		38
07 		39 	for {
08 			if _, err := conn.ReadMessage(); err != nil {
09 40 	break
10 type WSServer struct {41 	}
11 	log		42 	*zap.Logger
12 	Clients map[string]*websocket.Conn		43 	ws.ClientMutex.Lock()
13 	ClientsMutex sync.Mutex		44 	delete(ws.Clients, conn)
14 		45 	ws.ClientMutex.Unlock()
15 \func NewWSServer(log *zap.Logger) *WSServer {		46 	conn.Close()
16 	ws := &WSServer{		47
17 		tClients: make(map[string]*websocket.Conn)},		48 	
18 	}		49 	51 func (ws *WSServer) Notify(path string) {
19 	ws.Log.Debug("Notify", zap.String("path", path)) 50 	ws.ClientMutex.Lock()
20 	return err 51 	defer ws.ClientMutex.Unlock()
21
22 func (ws *WSServer) Handler(w http.ResponseWriter, r *http.Request) {		52 	others := ws.Clients
23 	conn, err := upgrader.Upgrade(w, r, nil) 53 	msg := map[string]string{"path": "path"}
24 	ws.CheckOrigin = func(r *http.Request) bool { return true }		54 	if err := json.Unmarshal(conn, &msg); err != nil {
25 	}		55 	conn.Close()
26
27 func(conn, err error) upgrader.Upgrade(r. nil) {		56 	delete(ws.Clients, conn)
28 	if err != nil {		57
29 	tws.Log.Error("Websocket", zap.error(err))		58
30 	return		59
```

在添加正体后不久。消息由 `ws.message` 事件处理器处理。传入的消息是 JSON 格式，包含了修改文件的路径和内容。代码随后根据修改文件的扩展名决定做什么。

第 54 行的指令确保了当设置了 `lock()` 时，当前函数会在 `lock()` 完成前执行。忘记重置是一个好主意，特别是当你正在处理复杂的 `if` 逻辑时。

### JavaScript 接收器

图 4 显示了 WebSocket 连接的客户端。如果 HTML 文件头包含此 JavaScript 代码段，浏览器将调用 `new` 来向 WebSocket 服务器打开连接。

### 列表 1: innotify.go

```go
01 package name 19 select {
02 case event, ok := <-watcher.Events
03 import 21 if ok {
04 "github.com/fsnotify/fsnotify" 22 return
05 } 23 }
06 30
07 func watchdirs(paths []string, cb func(string)) error { 24
08 watcher, err := fsnotify.NewWatcher() 25
09 if err != nil { 26
10 return err 27
11 } 28
12 29
13 if event.Op&fsnotify.Write == fsnotify.Write || fsnotify.Write == fsnotify.Create = 29
14 cb(event.Name) 30
15 31
16 for _, path := range paths { 31
17 watcher.Add(path) 32
18 } 32
19 33
20 func go() { 34
21 for { 35
22 return 36
```

### 列表 2: websocket.go

```go
01 package main		33 }
02 import		34 	ws.ClientMutex.Lock()
03 	"github.com/gorilla/websocket"		35 	ws.Clients[conn] = true
04 	"go.uber.com/zap"		36 	ws.ClientMutex.Unlock()
05 	"net/http"		37
06 	"sync"		38
07 		39 	for {
08 			if _, err := conn.ReadMessage(); err != nil {
09 40 	break
10 type WSServer struct {41 	}
11 	log		42 	*zap.Logger
12 	Clients map[string]*websocket.Conn		43 	ws.ClientMutex.Lock()
13 	ClientsMutex sync.Mutex		44 	delete(ws.Clients, conn)
14 		45 	ws.ClientMutex.Unlock()
15 \func NewWSServer(log *zap.Logger) *WSServer {		46 	conn.Close()
16 	ws := &WSServer{		47
17 		tClients: make(map[string]*websocket.Conn)},		48 	
18 	}		49 	51 func (ws *WSServer) Notify(path string) {
19 	ws.Log.Debug("Notify", zap.String("path", path)) 50 	ws.ClientMutex.Lock()
20 	return err 51 	defer ws.ClientMutex.Unlock()
21
22 func (ws *WSServer) Handler(w http.ResponseWriter, r *http.Request) {		52 	others := ws.Clients
23 	conn, err := upgrader.Upgrade(w, r, nil) 53 	msg := map[string]string{"path": "path"}
24 	ws.CheckOrigin = func(r *http.Request) bool { return true }		54 	if err := json.Unmarshal(conn, &msg); err != nil {
25 	}		55 	conn.Close()
26
27 func(conn, err error) upgrader.Upgrade(r. nil) {		56 	delete(ws.Clients, conn)
28 	if err != nil {		57
29 	tws.Log.Error("Websocket", zap.error(err))		58
30 	return		59
```

在添加正体后不久。消息由 `ws.message` 事件处理器处理。传入的消息是 JSON 格式，包含了修改文件的路径和内容。代码随后根据修改文件的扩展名决定做什么。

第 54 行的指令确保了当设置了 `lock()` 时，当前函数会在 `lock()` 完成前执行。忘记重置是一个好主意，特别是当你正在处理复杂的 `if` 逻辑。

### JavaScript 接收器

图 4 显示了 WebSocket 连接的客户端。如果 HTML 文件头包含此 JavaScript 代码段，浏览器将调用 `new` 来向 WebSocket 服务器打开连接。

### 列表 1: innotify.go

```go
01 package name 19 select {
02 case event, ok := <-watcher.Events
03 import 21 if ok {
04 "github.com/fsnotify/fsnotify" 22 return
05 } 23 }
06 30
07 func watchdirs(paths []string, cb func(string)) error { 24
08 watcher, err := fsnotify.NewWatcher() 25
09 if err != nil { 26
10 return err 27
11 } 28
12 29
13 if event.Op&fsnotify.Write == fsnotify.Write || fsnotify.Write == fsnotify.Create = 29
14 cb(event.Name) 30
15 31
16 for _, path := range paths { 31
17 watcher.Add(path) 32
18 } 32
19 33
20 func go() { 34
21 for { 35
22 return 36
```

### 列表 2: websocket.go
