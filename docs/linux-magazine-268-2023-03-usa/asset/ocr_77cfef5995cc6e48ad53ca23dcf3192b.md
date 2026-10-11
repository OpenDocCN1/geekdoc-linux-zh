# Programming Snapshot – Go and R

# IN-DEPTH

![](bbox=[0.0, 0.0, 0.18, 0.55])

# Exercise

The ZIP file containing the downloaded data includes a JSON file named \`StreamWithHistory.json\` with the metadata of all the streams you played in historical order (Figure 2). In addition to the song and artist, the entries also list the start date and time and the playback duration. Playback duration is particularly interesting because if the user interrupts a stream after a few seconds and fast forwards to the next song, the track probably made it onto the playlist by mistake and was something the user didn’t actually like. It will most likely turn out to be a false positive when it comes to putting together music suggestions.

JSON parser to create an internal Go data structure from the Spotify data, the format must be known and also match that of the actual JSON format. The JSON blob provided by Spotify, as shown in Figure 2, consists of an array whose elements each correspond to a streamed track. The artist and track names are stored as strings in the \`artistName\` and \`trackName\` fields. \`msPlayed\` gives you the playback time in milliseconds, while \`endTime\` has the date and time at the end of playback. The fields of the \`stream\` structure in Listing 1 each start with a capital letter, which means that other packages can also access them later on. However, this means that the names are not identical to the variable names in JSON format, each of which starts with a lowercase letter. However, this is no big deal, because Go lets you give a structure a name that can differ from the field name with the \`json:\` tag.

![](bbox=[0.07, 0.25, 0.3, 0.55])

For example, \`artistName\` string \`json:artistName\` in line 10 specifies that the artist in the \`artistName\` field is of the \`string\` type in the Go structure, and

# Listing 1: stats.go

```
```go
01 package main
02 import (
03     "encoding/json"
04     "fmt"
05     "log/ioutil"
06     "sort"
07 )
08 type stream struct {
09     EndTime     string `json:endTime`
10     ArtistName  string `json:artistName`
11     MsPlayed    int64  `json:msPlayed`
12     TrackName   string `json:trackName`
13 }
14 const jsonFile = "MyData/StreamingHistory0.json"
15 func main(){
16     bySong := map[string]int64{}
17     content, err := ioutil.ReadFile(jsonFile)
18     if err != nil {
19         panic(err)
20     }
21     data := []stream{}
22     err = json.Unmarshal(content, &data)
23     if err != nil {
24         panic(err)
25     }
26     for _, song := range data {
27         title := fmt.Sprintf("%s/%s", song.ArtistName, song.TrackName)
28         bySong[title] += 1
29     }
30     type kv struct {
31         Key   string
32         Value int64
33     }
34     kvs := []kv{}
35     for k, v := range bySong {
36         kvs = append(kvs, kv{k, v})
37     }
38     sort.Slice(kvs, func(i, j int) bool {
39         return kvs[i].Value > kvs[j].Value
40     })
41     for i := 0; i < 3; i++ {
42         fmt.Printf("%s (%dx)\n", kvs[i].Key, kvs[i].Value)
43     }
44 }
```
```

# Listing 2: Top Three Songs

Sparks/When Do I Get to Sing "My Way" – 2019 – Remaster (19x)

Falco/The Sound of Music (16x)

Linkin Park/With You (14x)