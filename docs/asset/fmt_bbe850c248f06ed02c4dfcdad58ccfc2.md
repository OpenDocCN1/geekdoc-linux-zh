
`THelloWorld`类包含了提供应用程序实现的属性和方法。这些属性和方法在主`HelloWorld`表单的事件处理器中被引用。由于这些元素本身不是视觉化的，取决于开发者为它们的使用创建实现和支持代码。相反，Kylix 允许开发者通过右键点击并选择“光标处补全类”`Shift+Ctrl+C`来自动完成类元素。Kylix 将完成代码，不仅通过为方法提供实现，还会完成属性的实现，包括属性访问器方法的实现（有关属性的更多信息，请参阅书的第 16 章“编写自定义组件”）。

> 提示：为了让 Kylix 能够完成属性定义，请确保在“工具|环境 选项”中勾选了“完成未完成的属性”。

```pas
unit HelloWorld;

interface

type

HelloWorld = class

private

    nCurrent: String;

    procedure SetCurrentLanguage(const Value: String);

public

    property CurrentLanguage:String read FCurrentLanguage write
        setCurrentLanguage;

    procedure SayHello;

    procedure SayWelcome;

end;

implementation

{ HelloWorld }

procedure HelloWorld.SayHello;

begin

end;

procedure HelloWorld.SayWelcome;

begin

end;

procedure HelloWorld.SetCurrentLanguage(const Value: String);

begin

    nCurrent := Value;

end;

end.
```
