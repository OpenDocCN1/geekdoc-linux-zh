```
cd ~/Documents
cat canada.txt
```

```
## Nunavut
## Quebec
## Northwest Territories
## Ontario
## British Columbia
## Alberta
## Saskatchewan
## Manitoba
## Yukon
## Newfoundland and Labrador
## New Brunswick
## Nova Scotia
## Prince Edward Island
```

This output from cat canada.txt will go into our pipe, and we’ll attach the dispensing end of the pipe to head, which we use to look at the first few lines of a file:

```
cat canada.txt | head -n 5
```

```
Nunavut
Quebec
Northwest Territories
Ontario
British Columbia
```