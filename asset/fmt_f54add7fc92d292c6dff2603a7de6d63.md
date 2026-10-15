
```
function SysRegisterIPlookup(StartAddr, EndAddr: LongInt; Context: Pointer;
GOT: LongInt): LongBool;

procedure SysunregisterIPlookup(StartAddr: LongInt);
function SysClosestDelphiHandler(Context: Pointer): LongWord;

function AreOSEExceptionsBlocked: Boolean;
procedure BlockOSEExceptions;
procedure UnblockOSEExceptions;

function ExceptObject: TObject;
function ExceptAddr: Pointer;

procedure Assert(expr : Boolean [: const msg: string]);
procedure Halt(Code: Integer);
procedure RunError(errorCode: Byte);
```

# 指数例程

```
function IntPower(const Base: Extended; const Exponent: Integer): Extended register;
function Power(const Base, Exponent: Extended): Extended;
```

# 文件 I/O 例程

```
function Append(var t: TTextRec): Integer;
function Assign(var t: TTextRec; const S: string): Integer;
procedure AssignFile(var F: Filename; string);
function BlockRead(var F: TFileRec; buffer: Pointer; recCnt: LongInt);
var recsRead: LongInt;

function BlockWrite(var F: TFileRec; buffer: Pointer; recCnt: LongInt);
var recsWritten: LongInt;

procedure Close(var F);
procedure CloseFile(var F);
function Eof(var F: Text): Boolean;
function Eol(var t: TTextRec): Boolean;
function Erase(var f: TFileRec);
function FilePos(var f: TFileRec): LongInt;
function FileSize(var f: TFileRec): LongInt;
function Flush(var t: TTextRec): Integer;
function IOResult: Integer;

procedure Read(var V1 [, V2,...,Vn]: Vn );
procedure Read([var F: Text]; V1 [, V2,...,Vn]);
procedure ReadLn(var t: TTextRec);
procedure Rename(var f: TFileRec; newName: PChar);
procedure Reset(var F: [File]; RecSize: Word );
procedure Rewrite(var F: [File]; RecSize: Word );
procedure Seek(var F: TFileRec; recCnt: Cardinal);
function SeekEof(var t: TTextRec): Boolean;
```

![](img/d784fa8294cae585d61ec86b987ea212_741_0.png)

# 附录 H：运行时例程

```
function SeekEol (var t: TTextRec) : Boolean;

procedure LineBreakStyle(var F: Text; Style: TTextLineStyle);

procedure SetTextBuf(var F: Text; var Buf [ ; Size: Integer );

procedure Truncate(var f: TFileRec);

procedure Write(var F: Text; P1 [ , P2...,Pn );

procedure Write(F, V1...,Vn);

procedure Writeln(var F: Text; P1 [ , P2..., Pn ) );
```
