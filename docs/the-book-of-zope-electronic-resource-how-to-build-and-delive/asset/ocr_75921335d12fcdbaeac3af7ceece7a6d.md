# Summary and Statistics Variables (continued)

| Name | Explanation |
| --- | --- |
| standard-deviation-nnn | The standard deviation of the numeric values calculated with a degree of freedom that comes after the [count-1] |
| standard-deviation-nnn | The standard deviation of the numeric values calculated with a degree of freedom that comes straight after the count |

# Special Element Grouping Variables

| Name | Explanation |
| --- | --- |
| first-nnn | Returns true if the current item is the first of the displayed items with the current value for the variable nnn; if not, it returns false. Used for grouping. |
| last-nnn | Returns true if the current item is the last of the displayed items with the current value for the variable nnn; if not it returns false. Used for grouping.

# Batch Processing Variables

| Name | Explanation |
| --- | --- |
| batch-start-index | The index (starting with 0) of the start of the current batch. |
| batch-end-index | The index (starting with 0) of the end of the current batch. |
| batch-size | The size of the current batch. |
| previous-sequence | Set to true on the first element of the batch if a batch precedes it. |
| previous-sequence-size | If previous-sequence is true, this is set to the number of elements in the previous batch. |
| previous-sequence-start-index | If previous-sequence is true, this is set to the start index of the previous batch. Used to construct previous-batch links. |
| next-sequence | Set to true on the last element of a batch if there is another batch after it. |
| next-sequence-size | If next-sequence is true, this is set to the number of elements in the next batch. |
| next-sequence-start-index | If next-sequence is true, this is set to the start index of the next batch. Used to construct links to the next batch. |
| sequence-query | The query string passed in the web request. Can be inserted into a link href to replay the query for a different batch. |