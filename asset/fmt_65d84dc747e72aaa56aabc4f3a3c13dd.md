
```pascal
if Assigned(Sender) then
  begin
    // 在此处做一些操作..
  end;
end;
```

### 3. 使用 `Assert` 验证假设为真的条件
`Assert` 使用得当是非常有用的。`Assert` 测试一个条件，如果条件为假，则抛出 `EAssertionFailed` 异常或产生运行时错误 227。当在应用程序中使用 `SysUtils` 时会抛出异常。

```pascal
// 仅用于演示
// 当在关闭断言的情况下编译时，
// 此函数仍然可能失败：
```

```pascal
function SafeIntegerDivide(num, denom : integer): integer;
begin
  Assert(denom <> 0, '分母不能为零!');
  Result := num div denom;
end;
```

当 `Assert` 检测到条件为假时，它会抛出一个异常，包含断言失败的完整路径、文件名和行号。上面的示例了如何在应用程序中使用断言。
通过指定适当的编译器指令（`{$S}-` 或 `$ASSERTIONS OFF`）从生成的代码中移除断言。由于它们通常从完成的构建中移除，断言不应取代值检查。示例说明了这一点。当断言关闭时会发生什么？如果 `denom` 变量为零，函数仍然会崩溃；它不是抛出断言异常，而是抛出除以零异常（`EDivByZero`）。

### 4. 使用 `try/except` 块妥善地捕获和处理异常
养成预期意外的习惯：捕获那些异常。

```pas
try
  // 执行一些事情
  // 此处有更多事情
  // 此处的某些地方一定会抛出异常
  // 在某地的某时间...
except
  // 此处有具体的异常处理器
  on e : exception do
    // 妥善处理异常。报告它、记录它等。
end;
```

### 5. 使用 `try/finally` 块保证即使发生异常也能释放资源
每当创建或打开资源时，自动使用 `try/finally` 块。

```pas
frm := TForm.Create(nil);
try
  if frm.ShowModal = mrOK
  begin
    // 采取适当的操作
  end;
finally
  fm.Free;
end;
```
