
```dart
void main() {
  runApp(CounterApp());
}

class CounterApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      ...
      home: MyHomePage(title: 'BLoC Pattern'),
      ...
    );
  }
}

class MyHomePage extends StatefulWidget {
  @override
  _MyPageState createState() => _MyPageState();
}

class _MyPageState extends State<MyHomePage>
  // 初始化 BLoC
  final CounterBloc _bloc; // 实现方式有所不同
  @override
  Widget build(BuildContext context) {
    ...
    body: Center(
```

```dart
child: (
  mainAxisAlignment: MainAxisAlignment.center,
  children: <Widget>[
    // Widget #6,
    // 使用 BLoC 状态流发出的更新状态
    // 构建 Widget #7
    // Widget #7,
  ],
),
  floatingActionButton: FloatingActionButton(
    // 将事件发送到 BLoC
    onPressed: () => _bloc.eventSink.add(CounterEvent.increment),
    tooltip: 'Increment',
    child: Icon(Icons.add),
  ),
}
@override
void dispose() {
  super.dispose();
  // 关闭 bloc 的流控制器以避免内存泄漏
  _bloc.dispose();
}
```

## CounterEvent

`CounterEvent` 枚举用于声明增加计数的事件。每当 FAB 被按下时，一个一个 `CounterEvent.increment` 事件就会被推送到事件流的 `sink` 中。

```dart
enum CounterEvent { increment }
```

## CounterState

`CounterApp` 只有一个状态，即计数器本身。在这种情况下，状态可以用 `int counter` 表示。计数器初始为 '0'，因此可以将其设置为 '0' 作为其初始状态。它声明在 `CounterBloc` 内部。

```dart
class CounterBloc {
  // 将计数器状态声明为 int
  int _counter = 0;
}
```

## CounterBloc

`CounterBloc` 类通过相应的 `StreamController`(s) 管理事件和状态流。它为事件和状态声明了 `StreamController`(s)、`Stream` 和 `Sink`。逐一查看这些部分，它们构成了一个 `CounterBloc` 类。每一步在图 19.4 中都用数字标记。

```dart
class CounterBloc {
  // 在 CounterBloc 中监听事件流
  CounterBloc() {
    // 设置事件的流
    // 设置状态的流
    // 映射事件到状态的业务逻辑
    // 关闭流控制器
  }
}
```

## StreamController

`StreamController` 管理事件流。它是一个事件类型的 `StreamController`。

```dart
final _eventController = StreamController();
```

## Event Sink

`eventSink` 是事件的 `sink`。它是 `eventController` 的 `sink`。

```dart
Sink<CounterEvent> get eventSink => _eventController.sink;
```

## StateController

`stateController` 管理输出流。它是 `int` 类型的 `StreamController`。

```dart
final _stateController = StreamController<int>();
```

## State Sink

`stateSink` 是状态的 `sink`。它是 `_stateController` 的 `sink`。

```dart
Sink<int> get stateSink => _stateController.sink;
```

## State Stream

`counter` 是状态流。它为监听的小部件提供更新的状态。

```dart
Stream<int> get counter => _stateController.stream;
```

## Mapping Event to State

`mapToState(CounterEvent event)` 方法将给定的事件映射到对应的状态。当传递增加类型时，`_counter` 增加一。

```dart
// 3. 映射事件到状态
void mapToState(CounterEvent event) {
  // 如果事件匹配则增加计数器
  if (event == CounterEvent.increment) {
    _counter++;
  }
  // 4: 将输出状态添加到 stateSink
  _stateSink.add(_counter);
}
```

# BLoC 设计模式

`child: Icon(Icons.add),`

)

# 重建组件/消费状态

这是根据给定事件的输出状态重新构建界面的最后一步。此步对应图 19.4 中的 #6。`StreamBuilder` 根据从 `bloc` 的 `StateController` 的流中收到的新状态构建 `Text` 小部件。通过将其 `stream` 属性赋值为 `_bloc.counter`，将 `bloc` 的输出流输入到 `StreamBuilder`。`snapshot` 携带输出状态，在本例中该状态为 `int` 类型。`snapshot` 显示更新后的计数器值。

```dart
//#6: StreamBuilder(
  stream: _bloc.counter,
  initialData: 0,
  builder: (BuildContext context, AsyncSnapshot<int> snapshot) {
    return Text(
      '${snapshot.data}',
      style: Theme.of(context).headline4,
    );
  })
```

## 在线源代码

本示例（第 19 章：基础 BLoC）的源代码可以在 GitHub 上找到。

# 改进后的 BLoC 模式实现

在本节中，我们将改进之前为 BLoC 定义事件和状态的实现。在上一节中，事件使用枚举声明，而状态被声明为 `int`。你将学习将事件和状态定义为类实现。当在构建复杂的应用时，状态/事件并不简单到可以用 `int` 或枚举表示时，这种实现非常有用。

## CounterEvent

`CounterEvent` 被声明为 `abstract`（抽象）类。在计划支持应用程序处理的多种事件时，这是一个良好的设计实践。在这种情况下，你只有增加事件，因此定义另一个扩展 `CounterEvent` 的子类 `IncrementEvent`。每当按下 FAB 时，一个 `IncrementEvent()` 事件就会推送到事件流的 `sink` 中。

```dart
abstract class CounterEvent {}
class IncrementEvent extends CounterEvent { }
```

## CounterState

计数器的状态使用 `CounterState` 类定义。它有一个 `int` 类型的 `counter` 变量，用于存储特定时刻的计数器值。工厂方法 `CounterState.initial()` 提供默认初始化为 '0' 的计数器状态。

```dart
class CounterState {
  final int counter;
  const CounterState({this.counter});
  factory CounterState.initial() => CounterState(counter: 0);
}
```

## CounterBloc
