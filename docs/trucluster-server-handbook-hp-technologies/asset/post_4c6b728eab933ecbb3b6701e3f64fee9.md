
# cat /etc/evmchannel.conf

# ==============================
# Event channel : binary error log
# ==============================
channel {
        name             binlog
        path             /usr/share/evm/channels/binlog
        events           @SYS_VIP.binlog
        fn_get           "binlog_get -r 8"
        fn_details       "binlog_details -decevent -ca localhost"
        fn_explain       "binlog_explain"
        fn_cleanup       "binlog_cleanup"
}
...

Before you ask, “What are those binlog2evm and binlogshow files?”...

# grep binlog2evm *

binlog_get:CONVTOOL=$DIR/binlog2evm                 # Converts binlog events to EVM events

# grep binlogshow *

binlog_details:CONVTOOL='${DIRNAME}$0' ./binlogshow

Finally, filters and templates are defined in the /usr/share/evm/filters/binlog.evf and /usr/share/evm/templates/sys/binlog.evt files (see sections 8.2.4 and 8.2.5).

One final note on channels: if you plan to define your own channel, place the definition in /etc/evmchannel.conf, but place the supporting files in the /var/evm/adm directory tree instead of /usr/share/evm.

## 8.2.4    EVM Filter Files

EVM filter files are located in the /usr/share/evm/filters directory (site-defined filter files should be placed in the /var/evm/adm/filters directory). Filter files should end with the suffix “.evf”.

See section 8.5 for additional information.

## 8.2.5 EVM Commands

Examples of using the EVM commands are in section 8.7, except for the evmreload(8) command, which was shown in section 8.2.2. EVM commands are shown in Table 8-2.

| Run?* | Command | Location | Man | Type | Description |
|---|---|---|---|---|---|
| ✓ | evmget | /usr/bin | 1 | binary | This program retrieves events from log files, and writes them to stdout in the form of binary EVM events. |
| ✓ | evminfo | /usr/bin | 1 | binary | This program provides information regarding the EVM subsystem. It also provides configuration file syntax verification. |
| ✓ | evmpost | /usr/bin | 1 | binary | This program allows posting of an event from the command line or script. It provides the ability for administrators and users to post quick (or simple) messages to EVM. |
| ✓ | evmshow | /usr/bin | 1 | binary | This program displays EVM events. |
| ✓ | evmsort | /usr/bin | 1 | binary | This program sorts EVM events. |
| ✓ | evmwatch | /usr/bin | 1 | binary | This program monitors the system or cluster for events to occur. It can also list the registered events that are known to the EVM subsystem. |
| ✗ | evmchmgr | /usr/sbin | 8 | binary | The evmchmgr program is the EVM channel manager. DO NOT RUN THIS PROGRAM ON THE COMMAND LINE. |
| ✗ | evmcommandset | /usr/sbin | - | sh | This shell script defines commands and their locations primarily for EVM's multi-platform implementation. |
| ✗ | evmd | /usr/sbin | 8 | binary | This program is the EVM daemon. DO NOT RUN THIS PROGRAM ON THE COMMAND LINE. |
| ✗ | evmget_srv | /usr/sbin | - | binary | The evmget_srv program is called by the evmd daemon when the evmget command requests retrieval of EVM events. |
| ✓ | evmlogger | /usr/sbin | 8 | binary | This program is the EVM logger. |
| ✗ | evmmkbin | /usr/sbin | - | binary | This program is used by the evmmkib command to compile the event templates into a binary format for the evmd daemon. |
| ✗ | evmmkib | /usr/sbin | - | sh | This script is used by evmd and the evmreload command to setup the environment for the evmkin program. |
|  | evmreload | /usr/sbin | 8 | sh | This shell script posts an event to have the EVM daemons reread their configuration files. It also verifies the syntax of event template files and configuration files. |
| ✓ | evmstart | /usr/sbin | 8 | sh | This shell script starts the EVM daemon. |
| ✗ | evmstop | /usr/sbin | 8 | sh | This shell script stops the EVM daemon, although it should not be run under normal circumstances. |

*The ✓ indicates that the program can be run. The ✗ indicates that the program should not be run.

# Table 8-2: EVM Commands
