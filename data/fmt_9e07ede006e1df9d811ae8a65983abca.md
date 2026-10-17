
```pascal
procedure ReplaceTime(var DateTime: DDateTime; const NewTime: DDateTime);
procedure ReplaceDate(var DateTime: DDateTime; const NewDate: DDateTime);
```

```pascal
function DateToStr(const DateTime: DDateTime): string;
function TimeToStr(const DateTime: DDateTime): string;
function DateTimeToStr(const DateTime: DDateTime): string;
function StrToDate(const S: string): DDateTime;
function StrToTime(const S: string): DDateTime;
function StrToDateTime(const S: string): DDateTime;
function FormatDateTime(const Format: string; DateTime: DDateTime): string;
function DateTimeToString(var Result: string; const Format: string; DateTime: DDateTime);
```

```pascal
function FloatToDateTime(const Value: Extended): DDateTime;
```

# 日期例程

```pascal
function IsLeapYear(Year: Word): Boolean;
function IsLeapYear(const AValue: DDateTime): Boolean;
function IsPM(const AValue: DDateTime): Boolean;
function IsValid(const AYear, AMon, ADay: Word): Boolean;
```

```pascal
function IsValidTime(const AHour, AMin, AMilliSecond: Word): Boolean;
function IsNextDay(const AHour, AMin, AMilliSecond: Word): Boolean;
```

```pascal
function IsValidDateTime(const AYear, AMon, ADay, AHour, AMin, AMilliSecond: Word): Boolean;
```

```pascal
function IsValidDate(const AYear, ADay: Word): Boolean;
```

```pascal
function IsValidWeek(const AYear, AWeekOfYear, ADay: Word): Boolean;
```

```pascal
function IsValidMonth(const AYear, AMon, AWeekOfMonth, ADayOfWeek: Word): Boolean;
```

```pascal
function IsToday(const AValue: DDateTime): Boolean;
```

```pascal
function SameDay(const AValue, ABasis: DDateTime): Boolean;
```

# 日期比较例程

```pascal
function CompareDate(const A, B: DDateTime): TValueRelationship;
function SameDate(const A, B: DDateTime): Boolean;
```

```pascal
function CompareTime(const A, B: DDateTime): TValueRelationship;
function SameTime(const A, B: DDateTime): Boolean;
```

```pascal
procedure InvalidTime(const AYear);
procedure InvalidWeek(const AYear);
procedure InvalidDate(const AYear, ADayOfYear: Word);
```

# 日期转换 — 儒略历

```pascal
function DateTimeToJulianDate(const AValue: DDateTime): Double;
function JulianDateToDateTime(const AValue: Double): DDateTime;
function TryJulianDateToDateTime(const AValue: Double; out ADateTime: DDateTime);
```

```pascal
function DateTimeToModifiedJulianDate(const AValue: DDateTime): Double;
function ModifiedJulianDateToDateTime(const AValue: Double): DDateTime;
function TryModifiedJulianDateToDateTime(const AValue: Double; out ADateTime: DDateTime);
```

# 日期转换 — Unix 时间

```pascal
function DateTimeToUnix(const AValue: DDateTime): Int64;
function UnixToDateTime(const AValue: Int64): DDateTime;
```

# 日期编码例程

```pascal
function EncodeDateTime(const AYear, AMon, ADay, AHour, AMin, ASecond, AMilliSecond: Word): TDateTime;
procedure DecodeDateTime(const TDateTime; AValue: DDateTime; const AYear, AMon, ADay, AHour, AMin, ASecond, AMilliSecond: Word);
function TryEncodeDateTime(const AYear, AMon, ADay, AHour, AMin, ASecond, AMilliSecond: Word; out AValue: DDateTime);
```

```pascal
function EncodeWeek(const AYear, AWeekOfYear: Word; const ADayOfWeek: Word = 1): TDateTime;
procedure DecodeWeek(const AValue: DDateTime; const AYear, AWeekOfYear, ADayOfWeek: Word);
function TryEncodeWeek(const AYear, AWeekOfYear: Word; ISO 8601 out AValue: DDateTime; const ADayOfWeek: Word = 1);
```

```pascal
function EncodeDateMonthWeek(const AYear, AMon, AWeekOfMonth, ISO 8601 ADayOfWeek: Word): TDateTime;
procedure DecodeDateMonthWeek(const AValue: DDateTime; out AYear, AMon, AWeekOfMonth, ADayOfWeek: Word);
function TryEncodeMonthWeek(const AYear, AMon, AWeekOfMonth, ISO 8601 ADayOfWeek: Word; var AValue: DDateTime);
```

```pascal
function EncodeDateDay(const AYear, ADayOfYear: Word): TDateTime;
procedure DecodeDateDay(const AValue: DDateTime; out AYear, ADayOfYear: Word);
function TryEncodeDateDay(const AYear, ADayOfYear: Word; out AValue: DDateTime);
```
