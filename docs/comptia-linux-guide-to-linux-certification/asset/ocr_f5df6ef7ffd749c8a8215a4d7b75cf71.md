![](bbox=[0.15, 0.08, 0.18, 0.21])

Another attractive feature of the vi editor is its ability to customize the user environment through settings that can be altered at the : prompt while in command mode. Simply type set all at this prompt to observe the list of available settings and their current values:

```
:set all
-- Options --
aleph=224		fileencoding=		menuitems=25		swapsync=fsync
noarabic		fileformat=unix		modeline		switchbuf=
arabicshape		filetype=		modelines=5			syntax=
noallowrevins		nofkmap		modifiable		tabstop=8
noaltkeymap		foldclose=		modified		tagsearch
ambiwidth=single	foldlevel=0		more			taglength=0
noautoident		foldenable=		mouse=			tagrelative
noautoindent		foldexpr=0		mousemodel=1		tagstack
noautowrite		foldignore=#		mousetime=500		term=xterm
noautowriteall	foldlevel=0		nonumber			notermbidi
background=light	foldlevelstart=-1	nopaste			termencoding=
backspace=2		foldmethod=manual	pastetoggle=		notext
nobackup		foldminlines=1		patchexpr=		textauto
backupcopy=auto	foldnestmax=20		patchmode=		noextmode
backupext=		formatoptions=tqc		nopreviewindent		textwidth=0
backupskip=/tmp/*	formatprg=		previewheight=12		thesaurus
nobinary		nogofile			nopreviewwindow		notilde
nobomb			helpheight=20		printdevice=		
timeout
bufhidden=		help/lang=en		printencoding=		timeoutlen=1000
buflisted		nohidden			printfont=			notitle
bufbyte=			history=50		printoptions=			titlelen=85
-- More --
```

Note in the preceding output that most settings are set to either on or off; those that are turned off are prefixed with a “no.” In the preceding example, line numbering is turned off (nonumber in the preceding output); however, you can turn it on by typing set number at the : prompt while in command mode. This results in the following output in vi:

```
1 Hi there, I hope this day finds you well.
2
3 Unfortunately we were not able to make it to your dining
4 room this year while vacationing in ALGONQUIN Park - I
```