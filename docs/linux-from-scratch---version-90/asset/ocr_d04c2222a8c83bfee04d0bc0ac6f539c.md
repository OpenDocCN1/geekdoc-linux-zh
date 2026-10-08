```
############################################################
# timespec()                                                     
# Purpose: An internal utility function to format a timestamp        
#   a boot log file. Sets the STAMP variable.                    

# Return value: Not used                                          
############################################################
timespec()
{
  STAMP=$(echo date +%b %d %T:%z` `hostname`) 
  return 0
}
```

```
############################################################
# log_success_msg()                                              
# Usage: log_success_msg ["message"]                                 
# Purpose: Print a successful status message to the screen and    
#   a boot log file.\                                              
# Inputs: $@ - Message                                            
# Return values: Not used                                          
############################################################
log_success_msg()
{
  /bin/echo -n -e "${BMPREFIX}${@}"
  /bin/echo -e "${CURSOR_ZERO}${SUCCESS_PREFIX}${SET_COL}${SUCCESS_SUFFIX}"
```

```
# Strip non-printable characters from log file      
logmessage=$(echo "${@}" | sed 's/\\\[a-zA-Z]\*.*//g')
ntimespec
/bin/echo -e "${STAMP} ${logmessage} OK" >> ${BOOTLOG}

  return 0
}
```

```
log_success_msg2()
{
  /bin/echo -n -e "${BMPREFIX}${@}"
  /bin/echo -e "${CURSOR_ZERO}${SUCCESS_PREFIX}${SET_COL}${SUCCESS_SUFFIX}"

echo "OK" >> ${BOOTLOG}

  return 0
}
```

```
################################################************
# log_failure_msg()                                               
# Usage: log_failure_msg ["message"]                                 
# Purpose: Print a failure status message to the screen and    
#   a boot log file.\                                              
# Inputs: $@ - Message                                            *
```