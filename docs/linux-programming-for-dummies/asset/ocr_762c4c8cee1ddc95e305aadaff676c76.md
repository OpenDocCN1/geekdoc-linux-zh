# **Table C-3**
**Statement Conversions**

| Statement | bash Shell Form | C Shell Form |
| :--- | :--- | :--- |
| if | if[ _condition_ ]<br>then<br>_command(s)_<br>fi | if (_condition_) then<br>_command(s)_<br>endif |
| if else | if [ _condition_ ]<br>then<br>_command_<br>else<br>_command(s)_<br>fi | if (_condition_) then<br>_command(s)_<br>else<br>_command(s)_<br>endif |
| if else if | if [ _condition_ ]<br>then<br>elif [ _condition_ ]<br>_command_<br>else<br>_command(s)_<br>fi | if (_condition_) then<br>_command_<br>elsif (_condition_)<br>_command(s)_<br>else<br>_command(s)_<br>endif |
| switch case | case variable in<br>case _value_:<br>_command(s)_<br>::<br>*)<br>esac | switch(_value_)<br>_command(s)_<br>breaksw<br>default:<br>_command(s)_<br>endsw |

# **Table C-4**
**Loop Command Conversions**

| Loop or Loop Command Function | bash Shell Form | C Shell Form |
| :--- | :--- | :--- |
| while | while [ _condition_ ]<br>do<br>_command(s)_<br>done | while (_condition_)<br>_command(s)_<br>end |
| foreach | for _variable_ in _list_<br>do<br>_command(s)_<br>done | foreach _variable_ (_list_)<br>_item(s)_<br>_command(s)_<br>end |
| Breaking out of a loop | break | break |
| Resuming a loop | continue | continue |