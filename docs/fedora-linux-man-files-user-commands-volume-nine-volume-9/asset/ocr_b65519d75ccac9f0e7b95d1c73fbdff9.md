# ARGUMENTS

pod2ht takes the following argunts:

+   - **help**
+       - `--help`
+   
+   Displays the usage ssage.
+   - **htdir**
+       - `--htdir=na`
+   
+   Sets the directory to which all cross references in the resulting HTML file will be relative. Not passing this causes all links to be absolute since this is the value that tells Pod::Ht the root of the docuntation tree.
+   Do not use this and —htroot in the sa call to pod2ht; they are tually exclusive.
+   - **htroot**
+       - `--htroot=URL`
+   
+   Sets the base URL for the HTML files. When cross-references are made, the HTML root is prepended to the URL.
+   Do not use this if relative links are desired; use—htdir instead.
+   Do not pass both this and —htdir to pod2ht; they are tually exclusive.
+   - **infile**
+       - `--infile=na`
+   
+   Specify the pod file to convert. Input is taken from STDIN if no infile is specified.
+   - **outfile**
+       - `--outfile=na`
+   
+   Specify the HTML file to create. Output goes to STDOUT if no outfile is specified.
+   - **podroot**
+       - `--podroot=na`
+   
+   Specify the base directory for finding library pods.
+   - **podpath**
+       - `--podpath=na:...:na`
+   
+   Specify which subdirectories of the podroot contain pod files whose HTML converted forms can be linked-to in cross-references.
+   - **cachedir**
+       - `--cachedir=na`
+   
+   Specify which directory is used for storing cache. Default directory is the current working directory.
+   - **flush**
+       - `--flush`