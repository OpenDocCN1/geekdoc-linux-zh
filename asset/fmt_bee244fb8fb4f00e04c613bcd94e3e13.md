
`declare variables`

`open files`

`print head1`

`print head2`

`read custRec`

![](img/cad5396e3e49a03edb322ef333cfad40_279_0.png)

`produceReport()`

`if lineCounter = 60 then`

`perform startPage()`

`print custLast, custFirst`

`lineCounter = lineCounter + 1`

`return`

### `startPage()`
`print head1`

`print head2`

`lineCounter = 0`

`return`

### `cleanUp()`
`close files`

`return`

`print head1`

`print head2`

`return`

`lineCounter = 0`

`return`
