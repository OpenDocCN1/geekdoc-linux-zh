
# Advanced Bash-Scripting Guide

```bash
IFS=${NO_WSP}
parent_child=(${parent_child[@]}) ${_den_pc[@]}
IFS=${_WSP}
fi

# Update list known_pair (Address and Name).
unique_lines _den_pair _den_pair
edit_exact known_pair[] _den_pair
if [ ${_den_pair[@]} -gt 0 ]; # Anything new?
then
  IFS=${NO_WSP}
  known_pair=(${known_pair[@]}) ${_den_pair[@]}
  IFS=${_WSP}
fi

# Update list of reverse pairs.
unique_lines _den_rev _den_rev
edit_exact reverse_pair[] _den_rev
if [ ${_den_rev[@]} -gt 0 ]; # Anything new?
then
  IFS=${NO_WSP}
  reverse_pair=(${reverse_pair[@]}) ${_den_rev[@]}
  IFS=${_WSP}
fi

# Check indirection limit give up if reached.
if ! _den_lmt=$(limit_chk[1])
then
  return 0
fi

# Execution define any LIFO. Order of pend operations is important.
# Did we define new addresses?
unique_lines _den_address _den_address
edit_exact known_address _den_address
edit_exact un_address _den_address
if [ ${_den_address[@]} -gt 0 ];
# Anything new?
then
  uc_address=(${uc_address[@]}) ${_den_address[@]}
  pend_func expand_input_address(${_den_lmt})
  trace_log[${_trace_log[@]]]='Add ${_den_address[@]}' unchkd addr.
  return 0
fi

# Did we find any new?
unique_lines _den_name _den_name
edit_exact known_name _den_name
edit_exact uc_name _den_name
if [ ${_den_name[@]} -gt 0 ];
# Anything new?
then
  uc_name=(${uc_name[@]}) ${_den_name[@]}
  pend_func expand_input_name(${_den_lmt})
  trace_log[${_trace_log[@]]]='Added ${_den_name[@]}' unchkd name.
  return 0
fi

# The parse-it-yourself delegate reply
# Input is the chk_address list.
detail_each_address<indirection_limit>
detail_each_address() {
  if [ ${_chk_address[@]} -gt 0 ]; || return 0
  unique_lines chk_address chk_address
}
```

## Appendix A. Contributed Scripts

```bash
edit_exact known_address chk_address
if [ ${chk_address[0]} -gt 0 ]
then
    known_address=${known_address[0]} ${chk_address[@]}
    unset chk_address[]
fi
```

```bash
# Application specific output functions # # #
# Pretty print the known pairs.
report_pairs() {
    echo
    echo 'Known network pairs.'
    col_print known_pair 2 5 30
}
```

```bash
if [ ${auth_chain[0]} -gt 0 ]
then
    echo
    echo 'Known chain of authority.'
    col_print auth_chain 2 5 55
fi
```

```bash
if [ ${reverse_pair[0]} -gt 0 ]
then
    echo
    echo 'Known reverse pairs.'
    col_print reverse_pair 2 5 55
fi
```

```bash
# Check an address against the list of blacklist servers.
# A good place to capture for GraphViz: address->status(server(reports))
# check_lists <ip_address>
check_lists() {
    if [ $# -eq 1 ]; then return 1
    local -a cl_fwd_addr
    local -a cl_rev_addr
    local -a cl_reply
    local -i cl_rc
    local -i _ls_cnt
    local cl_dns_addr
    local cl_lkup

    split -s ${1} cl_fwd_addr cl_rev_addr
    cl_dns_addr+=${dot_array[${cl_rev_addr}]}
    _ls_cnt+=${list_server[${1}]}
    echo 'Checking address '${1}'
    for (( $cl = 0 ; $cl < ${_ls_cnt}; $cl++ ))
    do
        cl_lkup+=${cl_dns_addr}${list_server[${cl}]}
        if short_text ${cl_lkup} ${cl_reply}
        then
            if [ ${cl_reply[0]} -gt 0 ]
            then
                echo ' Records from '${list_server[${cl}]}'
                address_hits[${address_hits[${1}]}]+=1 '${list_server[${cl}]}'
                hs_RC=2
            fi
        fi
    done
    for (( _cl = 0 ; _cl < ${cl_reply[0]}; _cl++ ))
    do
        echo
    done
    echo ' ${($_cl_reply[${clr}])'\ndone
    fi
    return 0
}

# The usual application glue #

# Who did it?
credits() {
    echo 'Advanced Bash Scripting Guide: isspammer.bash, v2'
}

# How to use it?
# See also, "Quickstart" at end of script.
usage() {
cat <<-'_usage_statement_'
The script isspammer.bash requires either one or two arguments.
1 May be one of:
a) A domain name
b) An IPv4 address
c) The name of a file with any addresses, one per line.
2 May be one of:
a) A blacklist server domain name
b) The name of a file with blacklist server name, one per line.
c) If not present, a default list of (free) blacklist servers is used.
d) If a filename of an empty file is given, blacklist lookup is disabled.
All output is written to stdout.

Return codes: 0 -> OK, 1 -> failure, 2 -> Something Blacklisted.
Requires the external program "dig". The domain lookup depth to limits.
Set the environment variable SPAMMER_LIMIT to change.
SPAMMER_LIMIT=0 means unlimited on the command-line.
If arg is an integer, the limit is set to that value and then the above rules are applied.
For development:
Setting the environment variable SPAMMER_DATA to a filename will cause the execution engine to log a function call.
_usage_statement_
The default list see: Blacklist servers:
declare -a default_servers
default_servers[0]='bl-spamhaus.org' # Conservative, well maintained
default_servers[1]='relays.ord.org' # open relays
default_servers[2]='bl.spamcom.net' # You can report spammers here
default_servers[3]='12.dbbl.net' # early detected system
default_servers[4]='dnsl.sorbs.net' # Various mail lists
default_servers[5]='list.dbl.org'
default_servers[6]='multitop.dbl.org'
default_servers[7]='unconfirmed.dbl.org'
```

```bash
# User input argument #1
setup_input() {
    if [ -e $1 ] && [ -r $1 ]; # Name of readable file
    then
        file_to_array $1 uc_name
        echo "Filename ${1} as input."
    else
        if is_address $1; # IP address?
        then
            uc_address=${1}
            echo "Starting with address ${1}"
        else
            # Must be a name.
            uc_name=${1}
            echo "Starting with domain name ${1}"
        fi
    fi
    return 0
}
```

```bash
# User input argument #2
setup_servers() {
    if [ -e $1 ] && [ -r $1 ]; # Name of a readable file
    then
        file_to_array $1 list_server
        echo "Filename ${1} as blacklist server list."
    else
        list_server=${1}
        echo "Using blacklist server ${1}"
    fi
    return 0
}
```

```bash
# User environment variable SPAMMER_TRACE
live_log_die() {
    if [ $SPAMMER_TRACE ]; # Wants trace log?
    then
        if [ ! -e $SPAMMER_TRACE ];
        then
            if touch $SPAMMER_TRACE 2>/dev/null
            then
                pend_func echo $(printf '%q\n') \
            fi
        fi
    fi
}
```

## Appendix A. Constructed Scripts

```bash
environment.variable SPAMMER_DATA
data_capture() {
if [ ${SPAMMER_DATA}= ]; # Wants a data dump?
if [ -e ${SPAMMER_DATA} ];
then
  if touch ${SPAMMER_DATA} 2>/dev/null
  then
    pend_func $(printf '%q\n') \
    'Unable to create data output file >${SPAMMER_DATA}'
    pend_release
    exit 1
  fi
  .dot_file=${SPAMMER_DATA}
  .dot_dump=dump_dot
else
  if [ ! -w ${SPAMMER_DATA} ];
  then
    pend_func $(printf '%q\n') \
    'Unable to write data output file >${SPAMMER_DATA}'
    pend_release
    exit 1
  fi
  .dot_file=${SPAMMER_DATA}
  .dot_dump=dump_dot
fi
fi
}

# Grope user specified arguments.
do_user_args() {
if [ $#-gt 0 ] && is_number $1;
then
  indirect=$1
  shift
fi}
```
