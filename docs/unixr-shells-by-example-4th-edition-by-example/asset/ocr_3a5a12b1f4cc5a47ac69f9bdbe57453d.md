| Feature | C/TC | Bourne | Bash | Korn |
|---|---|---|---|---|
| Programming Constructs (continued): | | | | |
| if/else/self | if (expression) then commands else if (expression) then commands else commands endif | if command then commands elif command then commands else commands fi | if command then commands elif command then commands else commands fi | if command then commands elif command then commands else commands fi |
| conditional | | | | |
| goto | goto label :label: | N/A | N/A | N/A |
| switch and case | switch ("$value") case pattern1: commands breaksw case pattern2: commands breaksw default: commands breaksw endsw | case "$value" in pattern1) commands ;; pattern2) commands ;; esac | case "$value" in pattern1) commands ;; pattern2) commands ;; esac | case "$value" in pattern1) commands ;; pattern2) commands ;; esac |
| Loops: | | | | |
| while | while (expression) commands end | while command do command done | while command do command done | while command do commands done |
| for/forach | foreach var (wordlist) commands end | for var in wordlist do commands done | for var in wordlist do commands done | for var in wordlist do commands done |