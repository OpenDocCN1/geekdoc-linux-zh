# 610 LATEX

```
\epsfsize=5cm % specifies the width of the next figure
\epsfsize=4cm % specifies the height of the next figure
\epsfile<file> % inserts the specified PostScript file
```

Application of the three \epsf... commands is relatively easy:
\epsfile(file) inserts a PostScript file into the document. If the size of the figure has not been previously specified by means of \epsfx/size, LaTeX scales the illustration in its original size. If only one size was specified, LaTeX scales the size in such a way that the proportions of the illustration remain as they originally were. Therefore, it is usually sufficient to execute only one of the two \epsfx/... commands.

Generally, figures are neither centered nor framed. When these features are required, centering can be achieved with \centerline and framing withfbox.
The following table gives some examples for commands inside the figure environment. Commands are also shown which allow you to insert an empty (framed, if required) instead of a figure, into which an illustration can be glued at a later stage (admittedly a fairly old-fashioned method). Some new commands can make their appearance: \rule<eb><h> generates a $b \times h$ black rectangle which is used here to make room for the illustration to be glued by means of an (invisible) vertical line. \framebox generates a framed rectangle of a width and height.

```
\centerline{% centered PostScript graphic
\epsfsize=30mm % no frame, 3 cm wide
\epsfile(online.eps) %%
\centerline{\fbox % centered PostScript graphic
\epsfsize=40mm % with frame, 4 cm high
\epsfile(online.eps)}} %%
\centerline{% empty centered frame
\framebox[4cm](ule(0cm)(3cm)) % 4 cm wide, 3 cm high
\rule(0cm)(3cm) % unramed empty space,
                               % 3 cm high
```

When several figures are to be placed side by side, several minipages may be placed inside the figure environment (see also page 605). The opposite case - the use of a figure environment inside a minipage - is not possible. Therefore it is not a trivial exercise to place a captioned figure alongside text. You can, however, place an unlabeled PostScript graphic into a minipage by directly using the \eps... commands without a figure environment.

```
\begin{figure}[h]
\begin{minipage}[t](6.1cm)
\centerline{\framebox[6cm](\rule(0cm)(4.1cm))}
\caption[labelables-b2]{An empty frame into which a picture
can be glued at a later stage.)}
\end{minipage}
\fill
\begin{minipage}[t](6cm)
```