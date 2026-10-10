| Data type | Description | Space needed |
|---|---|---|
| DOUBLE [ (M,D) ] [ZERO FILL] | Contains a double-precision, floating-point number of an average size. Values that are allowed include: −1.7976931348623157E+308 to −2.2250738585072014E−308 0 2.2250738585072014E−308 to 1.7976931348623157E+308. | Uses 8 bytes. |
| DOUBLE PRECISION | Same as DOUBLE. | Same as DOUBLE. |
| FLOAT (X) [ZERO FILL] | Contains a floating-point number. For a single-precision floating-point number, x can be less than or equal to 24. For a double-precision floating-point number, x can be between 25 and 53. The display size and number of decimals are undefined. | Uses 4 bytes if X is less than or equal to 24. Uses 8 bytes if X is greater than or equal to 25 and less than or equal to 53. |
| FLOAT [ (M,D) ] [ZERO FILL] | Contains a single-precision floating-point number. Values that are allowed include: −3.402823466E+38 to −1.175494351E−38 0 1.175494351E−38 to 3.402823466E+38. If the display value (n) is less than or equal to 24, the number is a single-precision floating-point number. | Uses 4 bytes. |
| INT [ (M) ] [UNSIGNED] [ZERO FILL] | Contains an integer of normal size. The range is −2147483648 to 2147483647 if it's signed, and 0 to 4294967295 if unsigned. | Uses 4 bytes. |
| INTEGER [ (M) ] [UNSIGNED] [ZERO FILL] | Same as INT. | Same as INT. |
| MEDIUMINT [ (M) ] [UNSIGNED] [ZERO FILL] | Contains an integer of medium size. The range is −8388608 to 8388607 if it's signed and 0 to 16777215 if unsigned. | Uses 3 bytes. |
| NUMERIC (M,D) [ZERO FILL] | Same as DECIMAL. | Same as DECIMAL. |
| REAL | Same as DOUBLE. | Same as DOUBLE. |