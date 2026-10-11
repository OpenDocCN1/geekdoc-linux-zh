# **Listing 7.2 Continued**

```
```
decclare    PRODUCT        # product name from data file
decclare -i CSALES         # country sales from data file
declear -i FSALES          # foreign sales from data file
decleare -rx REPORT_NAME="Sales Report" # report title
# Sanity Checks

if test ! -r "$DATA_FILE" ; then
       printf "$SCRIPT: the report file is missing-aborting\n" >&2
       exit 192
fi

# Generate the report

printf "Report created on %s by %s\n" "$DATE" "$LOGNAME"
printf "\n"
printf "%s\n" "$REPORT_NAME"
printf "\n"
printf "%-12s12s12s12s12s\n" "Product" "Country" "Foreign" "Total" "Average"
printf "%-12s12s12s12s12s\n" "___" "___" "___" "___" "___"

{ while read PRODUCT CSALES FSALES ; do
      let "ITEMS+=1"
      LINE_TOTAL=$(CSALES+FSALES)
      LINE_AVG=$((CSALES+FSALES)/2)
      printf "%-12s12d12d12d12d\n" "$PRODUCT" "$CSALES" "$FSALES" \
      "$LINE_TOTAL" "$LINE_AVG"
done } < $DATA_FILE
# Print report trailer

printf "%-12s12s12s12s12s\n" "___" "___" "___" "___" "___"
printf "Total number of products: $d\n" "$ITEMS"
printf "\n"
printf "End of report\n"

exit 0
```
```