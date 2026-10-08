
# Advanced Bash-Scripting Guide

```bash
if [ ! -e "$datafile" ]
then
  echo "\$datafile" does not exist!"
  exit $E_DATAFILE
fi
#
```

```bash
arith_mean() {
  local rt=0 # Running total.
  local am=0 # Arithmetic mean.
  local ct=0 # Number of data points.

  while read value; # Read one data point at a time.
  do
    rt=$(echo "scale=$SC; $rt + $value" | bc)
    ((ct++))
  done

  am=$(echo "scale=$SC; $rt / $ct" | bc)
  echo $am return $ct # This function "returns" TWO values!
  # Caution: This little trick will not work if $ct > 255!
  # To handle a larger number of data points,
  # simply comment the "return $ct" above.
  echo "\$datafile"
}
```

```bash
mean1=$1 # Arithmetic mean (passed to function).
n=$2 # How many data points.
sum2=0 # Sum of squared differences ("variance")
avg2=0 # Average of $sum2.
dev0=0 # Standard Deviation.
```

```bash
while read value; # Read one data line at a time.
do
  diff=$(echo "scale=$SC; $mean1" | bc)
  # Difference between mean. and data point.
  ndiff2=$(echo "scale=$SC; $diff * $diff" | bc) # Squared.
  sum2=$(echo "scale=$SC; $sum2 + $ndiff2" | bc) # Sum of squares.
done
```

```bash
avg2=$(echo "scale=$SC; $sum2 / $n" | bc) # Avg. sum of squares.
dev=$(echo "scale=$SC; sqrt($avg2)" | bc) # Square root =
echo $dev # Standard Deviation.
```

```bash
< "$datafile" # Rewinds data file.

mean=$(arith_mean); count=$? # Two returns from function!
std_dev=$(sd (sd $mean $count))
echo "Number of data points in \"$datafile\" = $count"
echo "Arithmetic mean (average) = $mean"
echo "Standard Deviation = $std_dev"
#
```

# Advanced Bash-Scripting Guide

exit

```bash
# This script could stand some drastic streamlining,
# but not at the cost of reduced legibility, please.
```

```bash
######################################
# A sample data file (sample.dat):

# 18.35
# 19.0
# 18.88
# 18.91
# 18.64

# $ sh sd.sh sample.dat
```

```bash
# Number of data points in "sample.dat" = 5
# Arithmetic mean (average) = 18.756000000
# Standard Deviation = .235380544
######################################
```

# Example A-38. A pad file generator for shareware owners

```bash
#!/bin/bash
# pad.sh
```

```bash
######################################
# PAD (xml) file creator
# Written by Mendel Cooper <thegrendel.abs@gmail.com>
# Released to the Public Domain.
######################################
# Generates a "PAD" descriptor file for shareware
# packages, according to the specifications
# of the ASP.
# http://www.asp-shareware.org/pad
######################################
```

```bash
# Accepts (optional) save filename as a command-line argument
if [ -n "$1" ]
then
nsavefile=$1
else
savefile=save_file.xml
fi
```

```bash
# = PAD file headers
HDR1="<xml version="1.0" encoding="Windows-1252"?>"
HDR2="XML_DIZ_INFO"
HDR3="MASTER_PAD_VERSION_INFO"
HDR4="<MASTER_PAD_VERSION>1.15</MASTER_PAD_VERSION>"
HDR5="<MASTER_PAD_INFO>Portable Application Description, or PAD
for short, it is a data set that is used by shareware authors
to provide information about users interested in their products.
To find out go to http://www.asp-shareware.org/pad
HDR6="</MASTER_PAD_INFO>"
######################################
```

# Appendix A. Contributed Scripts

```bash
fill_in ()
{
    if [ -z "$2" ]
then
        echo -n "$1?"      # Get user input.
else
        echo -n "$1 $2?"    # Additional query?
fi
}
```

```bash
read var                      # May paste to field.
# This shows how flexible "read" can be.

if [ -z "$var" ]
then
    echo -e "\t$1" >>$savefile  # Indent with 2 tabs.
    return
else
    echo -e "\t$var" >>$savefile
    return # Return length of string.
fi
```

```bash
check_field_length ()    # Check length of program fields.
{
    # $1 = maximum length
    # $2 = actual length
    if [ "$2" -gt "$1" ]
then
        echo "Warning: Maximum length of $1 characters exceeded!"
fi
```

```bash
clear                          # Clear screen.
echo "PAD File"
echo "----------------------"
```

```bash
# Write File Headers to file.
echo $HDR1 >>$savefile
echo $HDR2 >>$savefile
echo $HDR3 >>$savefile
echo -e $HDR4 >>$savefile
echo -e $HDR5 >>$savefile
echo $HDR6 >>$savefile
```

```bash
# Company_Info
echo "COMPANY INFO"
CO_HDR="Company_Info"
echo "$CO_HDR" >>$savefile
```

```bash
fill_in Company_Name
fill_in Address_1
fill_in Address_2
fill_in City
fill_in State
fill_in Zip_Code
fill_in Country
```

```bash
# If applicable:
fill_in ASP_Member "[Y/N]"
# fill_in ASP_Member_Number
# fill_in ASP_Member "[Y/N]"
fill_in Company_WebSite_URL
```

```bash
clear  # Clear between sections.

# Contact_Info
echo "CONTACT INFO"
CONTACT_HDR="Contact_Info"
echo "$CONTACT_HDR" >>$savefile
fill_in Author_First_Name
fill_in Author_Last_Name
fill_in Author_Email
fill_in Contact_First_Name
fill_in Contact_Last_Name
fill_in Contact_Email
echo "$CONTACT_HDR" >>$savefile
# END Contact_Info
```

```bash
# Support_Info
echo "SUPPORT INFO"
SUPPORT_HDR="Support_Info"
echo "$SUPPORT_HDR" >>$savefile
fill_in Sales_Email
fill_in Support_Email
fill_in General_Email
fill_in Sales_Phone
fill_in Support_Phone
fill_in General_Phone
fill_in Fax_Phone
echo -e "$SUPPORT_HDR" >>$savefile
# END Support_Info
```

```bash
echo "$CO_HDR" >>savefile
# END Company_Info
```

```bash
# Program_Info
echo "PROGRAM INFO"
PROGRAM_HDR="Program_Info"
echo "$PROGRAM_HDR" >>$savefile
fill_in Program_Name
fill_in Program_Release_Month
fill_in Program_Release_Day
fill_in Release_Year
fill_in Cost_Dollars
fill_in Cost_Other
fill_in Program_Type "[Shareware/Freeware/GPL]"
fill_in Program_Release_Status "[Beta, Major Upgrade, etc.]"
fill_in Install_Support
fill_in Program_OS_Support "[Win95/Win2k/Linux/etc.]"
fill_in Program_Language "[English/Spanish/etc.]"
echo;
```

```bash
echo "FILE INFO"
FILEINFO_HDR="File_Info"
echo "$FILEINFO_HDR" >>$savefile
fill_in Filename_Versioned
fill_in Filename_Previous
fill_in Filename_Generic
fill_in Filename_Long
fill_in File_Size_Bytes
fill_in File_Size_X
fill_in File_Size_MB
echo -e "$FILEINFO_HDR" >>$savefile
# END File_Info
```

```bash
# Expire_Info
echo "EXPIRE_INFO"
EXPIRE_HDR="Expire_Info"
echo "$EXPIRE_HDR" >>$savefile
fill_in Has_Expire_Info "Y/N"
fill_in Expire_Count
fill_in Expire_Based_On
fill_in Other_Info
fill_in Expire_Day
fill_in Expire_Year
echo -e "$EXPIRE_HDR" >>$savefile
# END Expire_Info
```

```bash
# Program_Info
echo "ADDITIONAL PROGRAM INFO"
fill_in Program_Change_Info
fill_in Program_Specific_Category
fill_in Program_Category
fill_in JAVA_VM "[Y/N]"
fill_in VB_Runtime "[Y/N]"
fill_in DirectX "[Y/N]"
echo -e "$PROGRAM_HDR" >>$savefile
# END Program_Info
```

```bash
# Program Description
echo "PROGRAM_DESCRIPTIONS"
PROGDESC_HDR="Program_Descriptions"
echo "$PROGDESC_HDR" >>$savefile

LANG="English"
fill_in Keywords ",comma + space separated"
echo
echo "*85, 80, 250, 450, 2000 word program descriptions"
echo "(may cut and paste into field)"
# It would be appropriate to compose the following
+# Char_Desc fields with a text editor,
+# then cut-and-paste the text into the answer fields.
echo
```

# Appendix A. Contributed Scripts

# Advanced Bash-Scripting Guide

```bash
echo "--------------------45 characters--------------------"
fill_in Char_Desc_45
check_field_length 45 "$?"
echo
fill_in Char_Desc_80
check_field_length 80 "$?"

fill_in Char_Desc_250
check_field_length 250 "$?"

fill_in Char_Desc_450
fill_in Char_Desc_2000

echo "$LANG" >>$savefile
echo "$PROGDESC_HDR" >>savefile
# END Program Description

clear
echo "Done."; echo;
echo "Save file is: \"$savefile\""
```

# Example A-39. A man page editor

```bash
#!/bin/bash
# maned.sh
# A rudimentary man page editor

# Version: 0.1 (Alpha, probably buggy)
# Author: Mendel Cooper <thegreendl.abs@gmail.com>
# Rel: 16 June 2008
# License: GPL
```

```bash
savefile=\ # Global, used in multiple functions
E_NOINPUT=90 # User input missing (error). May or may not

# ================= Markup Tags ================
TopHeader="TH"
NameHeader="SH NAME"
SyntaxHeader="SH SYNTAX"
SynopsisHeader="SH SYNOPSIS"
InstallationHeader="SH INSTALLATION"
DescHeader=".SH DESCRIPTION"
OptHeader=".SH OPTIONS"
FilesHeader="SH FILES"
EnvHeader="SH ENVIRONMENT"
AuthHeader="SH AUTHOR"
BugsHeader=".SH BUGS"
SeeAlsoHeader=".SH SEE ALSO"
BOLD=".B*"
# ======================================================
# Add more tags, as needed.
# See groff docs for markup meanings.
# ======================================================
```

```bash
start ()
{
clear            # Clear screen.
echo "ManEd"
echo "----"
}
```

```bash
fill_in ()
{
    if [ -z "$2" ]
then
        echo -n "$1?"      # Get user input.
else
        echo -n "$1 $2?"    # Additional query?
fi
}
```

```bash
read var                      # May paste to field.
# This shows how flexible "read" can be.

if [ -z "$var" ]
then
    echo -e "\t$1" >>$savefile  # Indent with 2 tabs.
    return
else
    echo -e "\t$var" >>$savefile
    return # Return length of string.
fi
```

```bash
check_field_length ()    # Check length of program fields.
{
    # $1 = maximum length
    # $2 = actual length
    if [ "$2" -gt "$1" ]
then
        echo "Warning: Maximum length of $1 characters exceeded!"
fi
```

```bash
# Write File Headers to file.
echo $HDR1 >>$savefile
echo $HDR2 >>$savefile
echo $HDR3 >>$savefile
echo -e $HDR4 >>$savefile
echo -e $HDR5 >>$savefile
echo $HDR6 >>$savefile
```
