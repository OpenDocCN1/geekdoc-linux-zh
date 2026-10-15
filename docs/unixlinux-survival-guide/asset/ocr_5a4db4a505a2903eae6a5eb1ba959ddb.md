```
#
#   parameters:  filename of XML file without
#               extension, e.g. testbook
#
########################################################

# Variables
DBOOK_PATH=/opt/sfw/share/docbook/docbook-xsl-1.66.1
MY_FOP=/opt/sfw/share/docbook/fop-0.20.5/fop.sh

echo Building $1.html $1.pdf

# clean up first
rm $1.fo $1.pdf

# HTML
xsltproc \
    -o $1.html \
    $DBOOK_PATH/html/docbook.xsl \
    $1.xml

# PDF
xsltproc \
    -o $1.fo \
    --stringparam fop.extensions 1 \
    --stringparam draft.mode no \
    --stringparam section.autolabel 1 \
    --stringparam admon.graphics 1 \
    --stringparam paper.type A4 \
    $DBOOK_PATH/fo/docbook.xsl \
    $1.xml

$MY_FOP -fo $1.fo -pdf $1.pdf

# EOF
```

You just need to modify the paths to match the respective system. The script contains all commands necessary to transform an XML file adhering to the DocBook standard into an HTML and a PDF document. The program xsltproc is part of the libxslt package. It is used to transform the XML file using the XSLT files. Listing 6.7 demonstrates the use of the script.