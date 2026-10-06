# $ cat list_cars
trap 'rm -f $$. > /dev/null;echo $0 aborted.;exit 1' 2 15
echo -n "Price range (for example, 5000 7500):"
read low hirange

echo

| Make | Model | Year (000) | Price |
| --- | --- | --- | --- | --- |
| gawk < cars ' | | | | |
| $5 >= 'lowrange' && $5 <= 'hirange' { | | | | $$.item |
| if ($1 - /plymouth/) $1 = "plymouth" | | | | |
| if ($1 - ~/chevrolet/) $1 = "chevrolet" | | | | |
| printf "-%10s %-8s %19yd %5d $ %8.2f\n", $1, $2, $3, $4, $5 | | | | |
| }' | sort -n +5 >> $$.item | | | |

cat $$.item
rm $$.item

# $ list_cars
Price range (for example, 5000 7500): 3000 8000

| Make | Model | Year (000) | Price |
| --- | --- | --- | --- | --- |
| chevrolet nova | 1979 | 60 | $ 3000.00 |
| chevrolet nova | 1980 | 50 | $ 3500.00 |
| honda accord | 1981 | 60 | $ 6000.00 |

# $ list_cars
Price range (for example, 5000 7500): 0 2000

| Make | Model | Year (000) | Price |
| --- | --- | --- | --- | --- |
| fiat | 600 | 1965 | 115 | $ 450.00 |
| toyota | tercel | 1982 | 180 | $ 750.00 |
| chevrolet | impala | 1965 | 85 | $ 1550.00 |

# $ list_cars
Price range (for example, 5000 7500): 10 0000

| Make | Model | Year (000) | Price |
| --- | --- | --- | --- | --- |
| ford | thundbd | 1984 | 10 | $ 17000.00 |

Error Messages

The following examples show some of the more common causes of gawk's infamous error messages (and nonmessages). The examples are run under bash. (When using gawk with other shells, the error message you get may be different).
The first example leaves the single quotation marks off the command line, so the shell interprets $3 and $1 as shell variables. Another problem is that there are no single quotation marks, the shell passes gawk four arguments instead of two: