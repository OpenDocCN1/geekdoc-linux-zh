# Hiew: goto.exe

| C:\Polygon\goto.exe | FRO ------- | a32 PE .00401000 |
|---|---|---|n| .00401000: 55 | push | ebp |
| .00401001: 88EC | mov | ebp,esp |
| .00401003: 680304000 | push | .00403000; 'begin' --E1 |
| .00401008: FF159204000 | call | printf |
| .0040100E: 83C404 | add | esp,4 |
| .00401011: EB0E | jmps | .00401021 --E2 |
| .00401013: 680304000 | push | .000403000; 'skip me!' --E3 |
| .00401018: FF159204000 | call | printf |
| .0040101E: 83C404 | add | esp,4 |
| .00401021: 681430400 | 2push | .00403014 --E4 |
| .00401026: FF159204000 | call | printf |
| .0040102C: 83C404 | add | esp,4 |
| .0040102F: 33C0 | xor | eax,eax |
| .00401031: 50 | pop | ebp |
| .00401032: C3 | retn ; -_A^-A_A^-A_A^-A_A^-A_A^-A_A_ |

11.1 Hiew