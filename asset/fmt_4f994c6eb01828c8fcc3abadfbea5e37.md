
```pascal
function StrLen(const Str: PChar): Cardinal;
function StrEnd(const Str: PChar): PChar;
function StrMove(Dest: PChar, const Source: PChar; Count: Cardinal): PChar;
function StrCopy(Dest: PChar, const Source: PChar): PChar;
function StrCopy(Dest: PChar, const Source: PChar): PChar;
function StrLCopy(Dest: PChar, const Source: PChar; MaxLen: Cardinal): PChar;
function StrPCopy(Dest: PChar, const Source: string): PChar;
function StrPLCopy(Dest: PChar, const Source: string; MaxLen: Cardinal): PChar;
function StrCat(Dest: PChar, const Source: PChar): PChar;
function StrLCat(Dest: PChar, const Source: PChar; MaxLen: Cardinal): PChar;
```

# Kylix 2 开发附录 H：运行时库例例

```pascal
function StrAlloc(Size: Cardinal): PChar;
function StrBufSize(const Str: PChar): Cardinal;
function StrNew(const Str: PChar): PChar;
procedure StrDispose(Str: PChar);
```

## 随机例例

```pascal
function Random((Range: Integer));
procedure Randomize;
function RandomRange(const AFrom, ATo: Integer): Integer;
function RandomFrom(const AValues: array of Integer): Integer; overload;
function RandomFrom(const AValues: array of Int64): Integer; overload;
function RandomFrom(const AValues: array of Double): Double; overload;
```

## 范围例例

```pascal
function EnsureRange(const AValue, AMin, AMax: Integer): Integer; overload;
function EnsureRange(const AValue, AMin, AMax: Int64): Integer; overload;
function EnsureRange(const AValue, AMin, AMax: Double): Double; overload;
```

```pascal
function InRange(const AValue, AMin, AMax: Integer): Boolean;
function InRange(const AValue, AMin, AMax: Int64): Boolean; overload;
function InRange(const AValue, AMin, AMax: Double): Boolean; overload;
```

## 矩形与点例例

```pascal
function EqualRect(const R1, R2: TRect): Boolean;
function Rect(Left, Top, Right, Bottom: Integer): TRect;
function Bounds(Aleft, Atop, AWidth, AHeight: Integer): TRect;
function Point(X, Y: Integer): TPoint;
function InRect(const TRect: TRect; const P: TPoint): Boolean;
function IntersectRect(out TRect: TRect; const R1, R2: TRect): Boolean;
function UnionRect(out TRect: TRect; const R1, R2: TRect): Boolean;
function IsRectEmpty(const TRect: TRect): Boolean;
function OffsetRect(var TRect: TRect; DX: Integer, DY: Integer;
```

## ELF 文件的资源例例

```pascal
function FindResource(ModuleHandle: HMODULE, ResourceName, ResourceType: PChar): TResourceHandle;
function LoadResource(ModuleHandle: HMODULE, ResHandle: THandle): HGLOBAL;
function SizeOfResource(ModuleHandle: HMODULE, ResHandle: THandle): Integer;
function LockResource(ResData: HGLOBAL): Pointer;
function UnlockResource(ResData: HGLOBAL): LongBool;
function FreeResource(ResData: HGLOBAL): LongBool;
```

## 运行时库附录 H：例例

## 资源字符串例例

```pascal
function LoadResourceString(ResRec: PHandle): string;
```

## 四舍五入与精度例例

```pascal
function Ceil(const X: Extended):Integer;
function Floor(const X: Extended):Integer;
```

```pascal
function RoundTo(const AValue: Double; const ADigit: TRoundTo): Double;
```

```pascal
function GetRoundMode: TRoundMode;
function SetRoundMode(const RoundMode: TRoundMode): TRoundMode;
```

```pascal
function GetPrecisionMode: TPrecisionMode;
function SetPrecisionMode(const Precision: TPrecisionMode): TPrecisionMode;
```

```pascal
function Int(X: Extended): Extended;
function Frac(X: Extended): Extended;
function Round(X: Extended): Int64;
function Trunc(X: Extended): Int64;
```

## 集合与序数例例

```pascal
procedure Exclude(var S: set of T; I:T);
procedure Include(var S: set of T; I:T);
function Pred(X);
function Succ(X);
```

```pascal
function Hi(X): Byte;
function High(X);
function Lo(X): Byte;
function Ord(X);
```

## 统计例例

```pascal
function Mean(const Data: array of Double): Extended;
function Sum(const Data: array of Double): Extended;
function SumInt(const Data: array of Integer): Integer;
function SumOfSquares(const Data: array of Double): Extended;
```

```pascal
procedure SumAndSquares(const Data: array of Double) var Sum, SumOfSquares:
Extended;
```
