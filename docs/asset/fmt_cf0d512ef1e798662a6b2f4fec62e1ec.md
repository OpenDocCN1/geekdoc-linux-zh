
```pascal
function YearSpan(const ANow: TDateTime, AThen: TDateTime): Double;
function MonthSpan(const ANow: TDateTime, AThen: TDateTime): Double;
function WeekSpan(const ANow: TDateTime, AThen: TDateTime): Double;
function DaySpan(const ANow: TDateTime, AThen: TDateTime): Double;
function HourSpan(const ANow: TDateTime, AThen: TDateTime): Double;
function MinuteSpan(const ANow: TDateTime, AThen: TDateTime): Double;
function SecondSpan(const ANow: TDateTime, AThen: TDateTime): Double;
function MilliSecondSpan(const ANow: TDateTime, AThen: TDateTime): Double;
```

# 目录管理程序

```pascal
function DirectoryExists(const Directory: string): Boolean;
function FindFirst(const Path: string; Attr: Integer; var F: TSearchRec);
function FindNext(var F: TSearchRec): Integer;
procedure FindClose(var F: TSearchRec);
```

```pascal
function ForceDirectories(Dir: string): Boolean;
function GetCurrentDir: string;
function SetCurrentDir(const Dir: string): Boolean;
```

```pascal
function CreateDir(const Dir: string): Boolean;
function RemoveDir(const Dir: string): Boolean;
```

# 附录 H：运行时库程序

```pascal
procedure ChDir(const S: string);
procedure GetDir(D: Byte; var S: string);
procedure MkDir(const S: string);
procedure RmDir(const S: string);
```

# 动态数组程序

```pascal
procedure DynArrayClear(var a: Pointer; typeInfo: Pointer);
procedure DynArrayLength(var a: Pointer; typeInfo: Pointer; dimcnt:
Longint; lengthVec: PLongint);
```

# 错误程序

```pascal
procedure Error(errorCode: RRuntime);
function GetLastError: Integer;
procedure SetLastError(errorCode: Integer);
```

# 异常处理程序

```pascal
function InquireSignal(RtISignal: Integer): TSignalState;
procedure AbandonSignalHandler(RtISignal: Integer);
function HookSignal(RtISignal: Integer);
procedure UnhookSignal(RtISignal: Integer; OnlyIfHooked: Boolean = True);
procedure HookOSEExceptions);
```

```pascal
function MapSignal(ISNum: Integer; Context: PSigContext): LongWord;
function SignalConverter(ExceptionIP: LongWord; FaultAddr: LongWord;
ErrorCode: LongWord);
```

```pascal
procedure SetSafeAllExceptionMsg(Msg: string);
function GetSafeCallExceptionMsg: string;
```

```pascal
procedure SetSafeAllExceptionAddr(Addr: Pointer);
function GetSafeCallExceptionAddr: Pointer;
```

```pascal
procedure Abort;
procedure OutOfMemoryError;
procedure RaiseLastError;
procedure ShowException(ExceptObject: TObject; ExceptAddr: Pointer);
function ExceptionErrorMessage(ExceptObject: TObject; ExceptAddr: Pointer;
Buffer: PChar; Size: Integer): Integer;
```

```pascal
function AcquireExceptionObject: Pointer;
procedure ReleaseExceptionObject;
```

```pascal
procedure GetUnwind(var Dest: TUnwind);
procedure SetUnwind(const NewUnwind: TUnwind);
function IsUnwindSet: Boolean;
```
