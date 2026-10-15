```
% egrep -v Kimberly\|Nabeel students
John Johnsen      john.johnsen@tp.com      503.555.1111
Hassaan Sarwar    hsarwar@k12.st.or       503.444.2132
David Kendall     d_kendall@msnbc.org     229.111.2013
John Johnsen      j.johnsen@psu.net       301.999.8888
Ibraheem Sarwar   ibraheem@abc.sci.com    222.123.4567
Maham Sarwar      smsarwar@k12.st.or     713.888.0000
Jamie Davidson    j.davidson@uet.edu      515.001.1212
Sandy Khan        sandy.khan@isu.edu     515.101.9009
%
```

The following command displays the lines in the students file that start with the letter J. Note the use of ^ to indicate the beginning of a line.

```
% egrep "^J" students
John Johnsen      john.johnsen@tp.com      503.555.1111
John Johnsen      j.johnsen@psu.net       301.999.8888
Jamie Davidson    j.davidson@uet.edu      515.001.1212
%
```

The following command displays the lines in the students file that start with the letters J or K. Note that ^J and ^K represent lines starting with the letters J and K.

```
% egrep "^J|^K" students
John Johnsen      john.johnsen@tp.com      503.555.1111
John Johnsen      j.johnsen@psu.net       301.999.8888
Kelly Kimberly    kellyk@umich.gov       555.123.9999
Jamie Davidson    j.davidson@uet.edu      515.001.1212
%
```

The egrep \^J\|^K students command could produce the same result. However, the egrep "^J"^K" students command uses simpler syntax. As a rule of thumb, if you need to escape multiple special characters in a regular expression, enclose the regular expression in single or double quotes, as the case may be.

In the following in-chapter exercises, you will use the commands of the grep family to understand their various characteristics.

# Exercise 7.11

Give a command for displaying the lines in the ~/Personal/Phones file that contain the words starting with the string David.

# Exercise 7.12

Give a command for displaying the lines in the ~/Personal/Phones file that contain phone numbers with area code 212. Phone numbers are stored as xxx-xxx-xxxx, where x is a digit from 0 to 9.