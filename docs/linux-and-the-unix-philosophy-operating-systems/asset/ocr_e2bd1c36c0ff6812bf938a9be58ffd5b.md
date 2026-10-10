| cp | A “fumble finger” front end to the Unix `cp` program that prevents you from unintentionally overwriting an existing file |
|---|---|
| l | Runs the `ls` command with the `-F` switch specified |
| ll | Runs the `ls` command with the `-l` switch specified |
| mv | Similar to the `cp` script, it prevents you from unintentionally overwriting an existing file by renaming another file to a file with the same name. |
| vit | Invokes the `vi` editor with the `-t` flag for use with tags and tag files. Tags make it easy to locate subroutines in a collection of files. |
| | \u00AE© 1984, Bell Telephone Laboratories, Inc. |

I have converted some scripts into aliases for use with the C shell, an interactive command interpreter originally found on Berkeley Unix systems. Aliases allow you to specify alternative forms of heavily used commands without having to resort to putting everything into shell scripts. Like shell scripts, they, too, are portable.

I originally built these tools under Unix Version 7 on a Digital PDP-11/70 at a small company engaged in the manufacture of newspaper composition systems. As the company added new systems for software development, I moved them to PDP-11/34, PDP-11/44, and LSI-11/23 systems also running Unix. This doesn't sound like a grand feat, given the renowned compatibility of the PDP-11 line, but wait. It gets better.

Eventually, I left the company in pursuit of other career opportunities, taking my tools with me on a nine-track tape. The C programs and shell scripts had soon found a home on a Digital VAX-11/750. The VAX-11/750 had more horsepower than the smaller PDP-11s I'd been using. Consequently, they ran a bit faster at the new company. The tools picked up even more speed when the company replaced the VAX-11/750 with a VAX-11/780. All this happened without modifications to the tools whatsover.

About that time, workstations—those wondrous you-mean-I-can-have-the-whole-darn-computer-to-myself boxes—vaulted onto the scene. Everyone flocked to buy the hot new machines from Sun Microsystems, my employer included. So the tools that had been moved from the PDP-11 to the VAX line suddenly found themselves running without modifications on Sun workstations.

Having spent the greater part of my software engineering career in New England, I found the latest equipment from the original digital equipment maker to be fairly common within a hundred miles of Boston. Again, I ported my old reliable C programs and shell scripts to the Digital line, this time to the VAX 8600 series and later to the VAX 8800 series. Again, the tools ran without modification.

Necessity is the mother of midnight invention. A software engineer I was working with had noticed a large cache of Digital Professional 350s collecting dust in a warehouse. An enterprising individual concluded that these 350s would make fine personal computers for us at home, especially if they were running Unix. So he proceeded to port a version of Unix