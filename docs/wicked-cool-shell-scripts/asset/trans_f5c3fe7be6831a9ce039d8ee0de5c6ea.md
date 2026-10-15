

```
condition`xmlint --xpath \
//response/current_observation/weather/text()\ 
<(echo $weather)

echo $state "($zip) : Current temp "$current"F and "$condition" outside."

exit 0
```

Listing 7-12: The weather script

## How It Works

In this script, we use curl to call the Wunderground API and save the HTTP response data in the weather variable ①. We then use the xmlint (easily installable with your favorite package manager such as apt, yum, or brew) utility to perform an XPath query on the data returned ②. We also use an interesting syntax in bash when calling xmlint with the <(echo $weather) at the end. This syntax takes the output of the inner command and passes it to the command as a file descriptor, so the program thinks it's reading a real file. After gathering all the relevant information from the XML returned, we print a friendly message with general weather stats.

## Running the Script

When you invoke the script, just specify the desired ZIP code, as Listing 7-13 shows. Easy enough!

## The Results

```
$ weather 78727
Austin, TX (78727) : Current temp 59.0F and Clear outside.
$ weather 80304
Boulder, CO (80304) : Current temp 59.2F and Clear outside.
$ weather 10010
New York, NY (10010) : Current temp 68.7F and Clear outside.
```

Listing 7-13: Testing the weather script

## Hacking the Script

We have a secret. This script can actually take more than just ZIP codes. You can also specify regions in the Wunderground API, such as CA/San_Francisco (try it as an argument to the weather script!). However, this format isn't incredibly user-friendly: it requires underscores instead of spaces and the slash in the middle. Adding the ability to ask for the state abbreviation and the city and then replacing any spaces with underscores if no arguments are passed would be a useful addition. As usual, this script could do with more error-checking code. What happens if you enter a four-digit ZIP code? Or a ZIP code that's not assigned?

## #59 Digging Up Movie Info from IMDb

The script in Listing 7-14 demonstrates a more sophisticated way to access the internet through lynx, by searching the Internet Movie Database (http://www.imdb.com/) to find films that match a specified pattern. IMDb assigns every movie, TV series, and even TV episode a unique numeric code; if the user specifies that code, this script will return a synopsis of the film. Otherwise, it will return a list of matching films from a title or partial title.

The script accesses different URLs depending on the type of query (numeric ID or file title) and then caches the results so it can dig through the page multiple times to extract different pieces of information. And it uses a lot—a lot!—of calls to sed and grep, as you’ll see.

### The Code

```
#!/bin/bash
# moviedata--Given a movie or TV title, returns a list of matches. If the user
#   specifies an IMDb numeric index number, however, returns the synopsis of
#   the film instead. Uses the Internet Movie Database.

titleurl="http://www.imdb.com/title/tt"
imdburl="http://www.imdb.com/find?s=tt&exact=true&ref_=fn_tt_ex&q="
tempout="/tmp/moviedata.$$"

summarize_film()
{
  # Produce an attractive synopsis of the film.
  grep "<title>" $tempout | sed 's/[<|>]*//g;s/(more)//'
  grep --color=never -A2 '<h5>Plot:' $tempout | tail -1 | \
    cut -d\< -f1 | fmt | sed 's/^/  /'
  exit 0
}

trap "rm -f $tempout" 0 1 15

if [ $# -eq 0 ] ; then
  echo "Usage: $0 {movie title | movie ID}" >&2
  exit 1
fi

########
# Checks whether we're asking for a title by IMDb title number

nodigits="$(echo $1 | sed 's/[[\digit:]]*/ /g')"

if [ $# -eq 1 -a -z "$nodigits" ] ; then
  lynx -source "$titleurl$1/combined" > $tempout
  summarize_film
  exit 0
fi
```

```
########
# It's not an IMDb title number, so let's go with the search...

fixedname="$(echo $0 | tr ' ' '+')"      # for the URL
url="$imdburl$fixedname"

⑧ lynx -source $imdburl$fixedname > $tempout

# No results?

⑨ fail="$(grep --color=never 'class="findHeader">No ' $tempout)"

# If there's more than one matching title...

if [ -z "$fail" ] ; then
echo "Failed: no results found for $1"
exit 1
elif [ ! -z "$(grep 'class="findHeader">Displaying' $tempout)" ] ; then
grep --color=never '/title/tt' $tempout | \
sed 's/<\/\n'
grep -vE '(\.png\.|jpg)\[\*\]' | \
grep -A 1 'a href="' | \
grep -v '^--$' | \
sed 's/<a <a href="\/title\/tt/g;s/<\/a>//' | \
⑩ awk '(NR % 2 == 1) { title=$0 } (NR % 2 == 0) { print title "  " $0 }' | \
sed 's/\/\/..\//: /' | \
sort
fi

exit 0
```

Listing 7-14: The moviedata script

### How It Works

This script builds a different URL depending on whether the command argument specified is a film title or an IMDb ID number. If the user specifies a title by ID number, the script builds the appropriate URL, downloads it, saves the lynx output to the $tempout file ⑧, and finally calls summarize_film() ⑩. Not too difficult.

But if the user specifies a title, then the script builds a URL for a search query on IMDb and saves the results page to the temp file. If IMDb can't find a match, then the <h2> tag with class="findHeader" value in the returned HTML will say No results. That's what the invocation at ⑨ checks. Then the test is easy: if $fail is not zero length, the script can report that no results were found.

