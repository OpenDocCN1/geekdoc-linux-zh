} except( CcCopyReadExceptionFilter( GetExceptionInformation(), &Status ) ) (

下面是一组过滤代码：

指令清单68.5 WRK-v1.2/base/ntos/cache/copysup.c

```
LONG
CcCopyReadExceptionFilter(
IN EXCEPTION_POINTERS ExceptionPointer,
IN NTSTATUS ExceptionCode
)
```

/*++ Routine Description:

This routine serves as a exception filter and has the special job of extracting the "real" I/O error when Mm raises STATUS_IN_PAGE_ERROR beneath us.

Arguments:

+   ExceptionPointer - A pointer to the exception record that contains the real Io.

+   ExceptionCode - A pointer to an NTSTATUS that is to receive the real status.

Return Value:

EXCEPTION_EXECUTE_HANDLER

```
/*--/
{
*ExceptionCode = ExceptionPointer->ExceptionRecord->ExceptionCode;
if (*ExceptionCode == STATUS_IN_PAGE_ERROR && (ExceptionPointer->ExceptionRecord->NumberParameters >= 3)) {
*ExceptionCode = (NTSTATUS)ExceptionPointer->ExceptionRecord->ExceptionInformation[2];
ASSERT(NT_SUCCESS(*ExceptionCode));

return EXCEPTION_EXECUTE_HANDLER;
}
```

从内部来看来说，SEH是由操作系统支持的异常处理扩展。但是异常处理函数属于exception_handler3(SEH3)或exception_handler4(SEH4)。而且代码依赖于MSVC编译器。它需要由MSVC的库文件或msvcr.dll的动态链接提供支持。SEH是由MSVC提供的一种机制，这一点至关重要。其他Win32的编译器的异常响应机制可能与SEH完全不同。

SEH3