```
```csharp
        // This code supports cancellation and progress reporting
        ct.ThrowIfCancellationRequested();
        if (progress != null) progress.Report(x * 10);
        await Task.Delay(1000); // Simulate doing something asynchronously
    }
    return DateTimeOffset.Now; // Ultimate return value
}

public IAsyncOperation<DateTimeOffset> DoSomethingAsync2() {
    // If you don't need cancellation & progress, use
    // System.WindowsRuntimeSystemExtensions' AsAsync[Action|Operation] Task
    // extension methods (these call AsyncInfo.Run internally)
    return DoSomethingAsyncInternal(default(CancellationToken), null).AsAsyncOperation();
}
#endregion

// After you ship a version, mark new members with a [Version(#)] attribute
// so that WinMDExp.exe puts the new members in a different underlying COM
// interface. This is required since COM interfaces are supposed to be immutable.
[Version(2)]
public void NewMethodAddedInV2() { }
}
```
```

以下 JavaScript 代码演示了如何访问前面的所有 WinRT 组件和功能。

```
```javascript
function () {
    // Make accessing the namespace more convenient in the code
    var WinRTComps = WinRTComponents;

    // NOTE: The JavaScript VM projects WinRT APIs via camel casing

    // Access WinRT type's static method & property
    var s = WinRTComps.WinRTClass.staticMethod(null); // NOTE: JavaScript pass "null" here!
    var struct = { anumber: 123, astring: "Jeff", aenum: WinRTComps.WinRTEnum.notNone };
    WinRTComps.WinRTClass.staticProperty = struct;
    s = WinRTComps.WinRTClass.staticProperty; // Read it back

    // If the method has out parameters, they and the return value
    // are returned as an object's properties
    var s = WinRTComps.WinRTClass.outParameters();
    var name = s.value; // Return value
    var struct = s.x; // an 'out' parameter
    var year = s.year; // another 'out' parameter

    // Construct an instance of the WinRT component
    var winRTClass = new WinRTComps.WinRTClass(null);
    s = winRTClass.toString(); // Call ToString()

    // Demonstrate throw and catch
    try { winRTClass.throwingMethod(); }
    catch (err) { }

    // Array passing
    var a = [1, 2, 3, 4, 5];
    var sum = winRTClass.passArray(a);

    // Array filling
    var arrayOut = [7, 7, 7]; // NOTE: fillArray sees all zeros!
    var length = winRTClass.fillArray(arrayOut); // On return, arrayOut = [0, 1, 2]

    // Array returning
    a = winRTClass.returnArray(); // a = [ 1, 2, 3]

    // Pass a collection and have its elements modified
    var localSettings = Windows.Storage.ApplicationData.current.localSettings;
```
```