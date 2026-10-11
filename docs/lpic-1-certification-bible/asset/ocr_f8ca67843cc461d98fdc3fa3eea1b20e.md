The cat utility can also be used to display the contents of a text file. These utilities aren't filters but are often helpful when working with them.

# ## Deleting or substituting characters

There are times when you may want to search a document for specific characters and then either delete or replace them. An example of this use would be a document that contains both uppercase and lowercase characters, but you would prefer all characters to be lowercase. The `tr` utility provides this functionality using the following syntax:

```
tr option set1 set2
```

The options used with `tr` are shown in Table 4-7.

| Option | Use | 
| :--- | :--- | 
| -d | Deletes the characters specified. | 
| -s | Replaces a sequence of characters with one character. | 
| --help | Displays help information and then exits. | 
| --version | Displays version information and then exits. |

The following is an example of the use of the `tr` utility. First, the contents of the file are viewed using the `more` utility. The file contains a mixture of both uppercase and lowercase characters. In an effort to avoid confusion all uppercase characters are replaced with their lowercase equivalents using the `tr` utility.

```
# more
mkdir MyFiles
cd MyFiles
ls -al MyFiles > AllofMyFiles
# tr 'A-Z' 'a-z' < mycommands
mkdir myfilescd myfiles
ls -al myfiles > allfmyfiles
```