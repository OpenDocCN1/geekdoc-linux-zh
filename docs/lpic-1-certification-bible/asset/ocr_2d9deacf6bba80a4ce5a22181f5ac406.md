| Command | Function |
| :--- | :--- |
| `lpg printer [options]` | Executes the `lpc` command from inside of `lpc`. Works only with LPRng. |
| `lprm printer jobid [jobid]*` | Executes `lprm` from inside of `lpc`. Works only with LPRng. |
| `move printer [ jobid ] destinationPrinter` | Moves the specified jobs to the destination printer, and removes them from the existing queue. Works only with LPRng. |
| `msg printer message text` | Updates the status message for the printer. Works only with LPRng. |
| `nohoidall ( all \| printer* )` | Disables automatic job holding started by `hoidall`. Works only with LPRng. |
| `redirect [printer [destinationPrinter \| off ]]` | Redirects jobs from the specified printer to the new destination printer. Use the `off` parameter to turn off redirection. Works only with LPRng. |
| `redo [printer [jobid]]` | Reprints the specified job. Works only with LPRng. |
| `release [printer [jobid]]` | Releases the selected held job for printing. Works only with LPRng. |
| `reread [ printer [\@host] ]` | Instructs `lpd` to reread the printcap file. Works only with LPRng. |
| `restart ( all \| printer )` | Starts a new printer daemon. |
| `server ( all \| printer )` | Shows the printcap entries for the specified printer(s). Works only with LPRng. |
| `start [all\|printer name]` | Enables the spool and starts the print daemon for the specified printer(s). |
| `status [printer name]` | Displays the status of the printer and queue. |
| `stop [all\|printer name]` | Stops the spooling daemon after the current job is completed and then disables printing for this printer. |
| `topg <printer> [Job number...] [user...]` | Places the jobs in the order you list at the top of the printer queue. |
| `up (all\|printer name)` | Enables printing and spooling and starts a printing daemon. |


Command-line options for the LPRng `lpc` are shown in Table 12-3.