# Advanced Bash-Scripting Guide

programmable completion features"
return

```
shopt -s extglob      # Necessary.
complete -A hostname      rsh rcp teinet login ftp ping disk
complete -A export        printnew
complete -A variable      export locally unset
complete -A enabled       builtin
complete -A alias        alias unalias
complete -A function      function
complete -A user          su mail finger

complete -A heliptopic    help      # Currently as builtins.
complete -A shot         shop
complete -A stopped -P '*'  bg
complete -A job -P '*'     fg jobs joined

complete -A directory     mkdir rmdir
complete -A directory     -o default cd

complete -f -o default -X '*,.*(zip|ZIP)'  zip
complete -f -o default -X '**,,.*(zip|ZIP)'  unzip
complete -f -o default -X '*,.*(GZ)'      compress
complete -f -o default -X '*,.*(gz)'      uncompressed
complete -f -o default -X '*,.*(gz|GZ)'  gzip
complete -f -o default -X '*,.*(gz)'      gunzip
complete -f -o default -X '*,.*(bz2|BZ2)'  bzip2
complete -f -o default -X '*,.*(ZIP|z|G|Gz|bz2|BZ2)'  extract
```

# Documents - Postscript,pdf,...
complete -f -o default -X '*,.*(ps|PS)'  gs ghostview ps2pdf ps2ascii
complete -f -o default -X '*'
'*,.*(dvi|DVI)' ddvips xxdvi dvips diselect dvtype
complete -f -o default -X '*,.*(pdf|PDF)'  acroead pdf2ps
'(.gz,.GZ,.bz2|BZ2).'*,.*(?|@(@(es|ps)? [ES] [pdf|PDF])?'
complete -f -o default -X '*,.*(tex|TEX)'  makeinfo text2dpi text2html text2pdf
complete -f -o default -X '*,.*(tex|TEX)'  tex latex latex
complete -f -o default -X '*,.*(lyx|LYX)'  lyx html2ps
complete -f -o default -X '*,.*(htm|HTML)'  lynx html2ps
complete -f -o default -X '*'
'*,.*(doc|DOC|xls|XLS)?'*,.?(PPT|XPS|CSV|OD|OD?|OTT)?'  soff

# Multimedia

```
complete -f -o default -X '*,.*(GIF|gif|JPG|JPG|BMP|BMP|xpm|xpm|png|PNG)' xmv mp ggview
complete -f -o default -X '*,.*(mp3|MP3)'  mpg123 mpg321
complete -f -o default -X '*,.*(ogg|OGG)'  ogg
complete -f -o default -X '*'
'!@.(MP3|MP3) [ogg|OGG|WAV|WAV]pl|\
u3|um|m|mod|s|3|mit|||flulc|flac)'  xms
complete -f -o default -X '*,.*(?|e|G|MP?(E|G)|wma|avi|AVI|
asf|vob|VOB|dat|vcd|ps|fi|fliv|vim|ram|yuv|mov|MOV|qt|
QT|mp3|MP3) [ogg|OGG|OGM|OGM|MP4|MP4|WAV|WAV|ASX|ASX]'  xine
```