
in,the,past,or,the,present

completely,unrelated,line1

in,the,past,or,the,present

completely,unrelated,line2

### 列表 4.57: data2.csv

in,the,past,or,the,present

completely,unrelated,line2

for,the,past,or,the,future

completely,unrelated,line3

### 列表 4.58: checksums.sh

列表 4.58 之所以查找第 2、5 和 7 列中字符串 `"past"` 的出现情况，是因为以下代码段：

```awk
(FNR==2 || FNR==5 || FNR==7) {
  if ($3 ~ "past") count++
}
```

如果发生匹配，`count` 的值就会加1。`END` 块报告该字符串在第 2、5 和 7 列中被找到的次数。注意，粘贴的字符串将匹配该字符串。列表 4.58 的输出为：

```
List of files: data1.csv data2.csv

past: matched 5 times
```

## 常见的排序算法

排序算法在性能方面有最好情况、平均情况和最坏情况。有趣的是，有时高效的算法（如快速排序）在给定数组已经排序时性能可能反而最差。以下子节包含了常见排序算法的代码示例：

- 冒泡排序 (`bubble sort`)
- 选择排序 (`selection sort`)
- 插入排序 (`insertion sort`)
- 合并排序 (`merge sort`)
- 快速排序 (`quick sort`)
- 桶排序 (`bucket sort`)
- 壳排序 (`shell sort`)
- 堆排序 (`heap sort`)
- 原地排序 (`inplace sort`)
- 计数排序 (`counting sort`)
- 基数排序 (`radix sort`)

如果你想深入探索排序算法，请执行额外的算法。

## 冒泡排序

冒泡排序涉及嵌套循环，数组的每个元素与其右侧的元素进行比较。如果数组元素小于当前元素，则交换值，这意味着数组的内容最终将完成排序。这里有一个例子：

```bash
arr1 = [40, 10, 30];
Item = 40;
Step 1: 40 > 10 so switch elements:
arr1 = [10, 40, 30];
Item = 40;
Step 2: 40 > 30 so switch elements:
arr1 = [10, 30, 20];
Item = 40;
Step 3: 40 > 20 so switch elements:
arr1 = [10, 20, 40];
```

如所示，最小元素位于数组 `arr1` 的左侧。通过将第二个位置（索引为 1）与右侧元素比较来重复此过程：

```bash
arr1 = [10, 30, 20, 40];
Item = 30;
Step 4: 30 > 20 so switch elements:
arr1 = [10, 20, 30, 40];
```

数组 `arr1` 现在是升序的（从左到右）。如果你想反转顺序使数组按降序排序（从左到右），只需将运算符 `>` 替换为 `<`。列表4.59 显示了 `bubble_sort.sh` 的内容，展示了如何使用冒泡排序对数字数组进行排序。

### 列表 4.59: bubble_sort.sh

```bash
echo " | awk |
BEGIN {
arr[0] = 30; arr[1] = 40; arr[2] = 200; arr[3] = -13;
printf("Array: ")
for (i=0;i<length(arr);i++) {
  printf("%d ",arr[i])
}
print ""
}
for (i=0;i<length(arr)-1;i++) {
  for (j=i+1;j<length(arr);j++) {
    if (arr[i] > arr[j]) {
      tmp = arr[i]
      arr[i] = arr[j]
      arr[j] = tmp
    }
  }
}
END {
printf("Sorted: ")
for (i=0;i<length(arr);i++) {
  printf("%d ",arr[i])
}
print ""
}
```
```

你可以手动执行列表 4.59 中的代码来说服自己代码是正确的（提示：是相同的步骤

（你之前在本节中看到的内容）。运行列表 4.59 中的代码，你将看到以下输出：

```
Array:    30 10 200 -13
Sorted:  -13 10 30 200
```

## 在单词列表中查找异字母位词

记住，如果 `word2` 是 `word1` 的排列，那么变量 `word1` 就是 `word2` 的异字母位词。列表 4.60 显示了 `anagram.sh` 的内容，它演示了如何检查两个单词是否互为异字母位词。

### 列表 4.60: anagram2.sh

```awk
echo " | awk '
function sort_word(strl) {
    split(strl,chars,"")
    word = ""
    for (idx in chars) {
        word = word chars[idx]
    }
    return word
}
function is_anagram(strl, str2) {
sorted1 = sort_word(strl)
sorted2 = sort_word(str2)
    return sorted1 == sorted2
}
BEGIN {
PROCINFO("sorted_in"]@val_str_asc")
words[1] = "abc"; words[2] = "evil"
words[3] = "z2"; words[4] = "cab"
words[5] = "live"; words[6] = "xyz"
words[7] = "zyx"; words[8] = "bac"
}
for (i=1; i<length(words)-1; i++) {
    for (j=i+1; j<length(words); j++) {
        result = is_anagram(words[i], words[j])
        if (result == 1) {
            printf("%10s and %10s => anagrams\n",
                words[i],words[j])
        } else {
            printf("%10s and %10s => not anagrams\n",
                words[i],words[j])
        }
    }
}
```

列表 4.60 定义了函数 `is_anagram()`，该函数接收参数 `str1` 和 `str2`，其排序后的值分别用于初始化变量 `sorted1` 和 `sorted2`。该函数返回比较 `sorted1` 和 `sorted2` 的结果：如果它们相等，则 `str1` 是一个回文。

列表 4.60 的下一部分部分将变量 `words` 初始化为字符串列表，紧接着是一个嵌套循环。外部循环使用变量 `i` 范围从 0 到 `len(words)-1`，内部循环使用变量 `j` 范围从 `i+1` 到 `len(words)`。内部循环将变量 `result` 初始化为调用函数 `is_anagram()` 返回的数值，该调用的参数为字符串 `words[i]` 和 `words[j]`。如果值 `result` 为 `True`，则这两个单词互为异字母位词。运行列表 4.60 中的代码，你将看到以下输出：

```
abc and evil => not anagrams
abc and Z => not anagrams
abc and cab => anagrams
abc and live => not anagrams
abc and xyz => not anagrams
abc and zyx => not anagrams
evil and Z => not anagrams
evil and cab => not anagrams
evil and live => anagrams
evil and xyz => not anagrams
evil and zyx => not anagrams
zand and cab => not anagrams
zand and live => not anagrams
zand and xyz => not anagrams
zand and zyx => not anagrams
cab and live => not anagrams
cab and xyz => not anagrams
cab and zyx => not anagrams
live and xyz => not anagrams
live and zyx => not anagrams
xyz and zyx => not anagrams
xyz and x => anagrams
```

## 以 O(n) 复杂度排序数组

列表 4.61 显示了 `simple_sort.sh` 的内容，向你展示了如何使用冒泡排序数组。

### 列表 4.61: simple_sort.sh

```awk
echo "" ' BEGIN {
arr1[1] = 0; arr1[2] = 1; arr1[3] = 2;
arr1[4] = 2; arr1[5] = 1; arr1[6] = 0;
arr1[7] = 0; arr1[8] = 1; arr1[9] = 2;
{
printf("Initial: ");
for(i=1; i<=length(arr1); i++)
  printf("%s ",arr1[i])
print ""
```
```awk
for(i=1; i<=length(arr1); i++) {
  if(arr1[i] == 0)
    zeros += 1
}
third = int (length(arr1)/3)
for(i=1; i<=third; i++) {
  arr1[i] = 0
  arr1[third+i] = 1
  arr1[2*third+i] = 2
}
```
```awk
printf("Sorted: ")
for(i=1; i<=length(arr1); i++) {
  printf("%s",arr1[i])
}
print ""
```

列表 4.61 利用包含多个 0、1 和 2 的列表 `arr1`，然后显示 `arr1` 的内容。第二个循环计算值 0 出现的次数。第三个循环使用“三分”技术将值 0、1 和 2 分配到连续的位置：所有的 0 值在前，然后是 1 值，最后是 2 值。任务中的关键词是“相等”，显示在该部分的顶部。列表 4.61 你将看到以下输出：

Initial: 0 1 2

Sorted: 0 1 2

## 数字数组的中位数

与其使用冒泡排序，可以使用 awk 内的 `sort()` 函数对数字或字符串排序。列表 4.62 显示了 `median1.sh` 的内容，展示了如何使用内置 `sort()` 函数找到数组的中位数。

### 列表 4.62: median1.sh

```awk
echo " | awk ' BEGIN {
arr1[1] = 400
arr1[2] = 5
arr1[3] = 1
arr1[4] = 123
arr1[5] = 500
arr1[6] = -55

print "=> Initial array:"
for(i=1; i<=length(arr1); i++) print ":",arr1[i]
}
END {
row_count = asort(arr1,arr2)

print "=> Sorted array"
for(i=1; i<=length(arr2); i++) print ":",arr2[i]

if (row_count % 2 != 0) {
    middle = int(row_count/2 + 0.5)
    median = arr2[middle]
} else {
    median = (arr2[row_count/2]+arr2[row_count/2+1])/2
}
print "=> Median value:",median
```

列表 4.62 起于一个 awk 命令，其中包含一个初始化 `arr1` 为多个值并显示其内容的语句。列表 4.62 的下部分调用内置 `sort()` 函数来填充数组 `arr2`，随后是确定中位数的条件逻辑。记住，奇数个数数组的中位数是数组中间的值，而偶数个数数组的中位数是数组两个“中间值”的平均值。`END` 语句中的最后片段显示数组的中位数。运行列表 4.62 中的代码，你将看到以下输出：

```
=> Initial array:
1 : 400
2 : 5
3 : 1
4 : 123
5 : 500
6 : -55
=> Sorted array:
1 : -55
2 : 1
3 : 5
4 : 123
5 : 400
6 : 500
=> Median value: 64

## 线性搜索

列表 4.63 显示了 `linear_search.sh` 的内容，展示了如何使用冒泡排序搜索数字数组。

### 列表 4.63: linear_search.sh

```awk
echo "" | awk ' BEGIN {
  item = 123
  arr1[1] = 1
  arr1[2] = 3
  arr1[3] = 5
  arr1[4] = 123
  arr1[5] = 400
}
{
  found = -1
  for(i=1; i<=length(arr1); i++) {
    if (item == arr1[i]) {
      found = i
      break
    }
  }
  if (found >= 0) {
    print "found",item,"in position"
  } else {
    print item,"not found"
  }
}
```

列表 4.63 起于一个 awk 命令，包含一个 `BEGIN` 语句初始化 `arr1` 为多个值并显示其内容。列表 4.63 的后续部分检查 `arr1` 中的值。如果 `item` 匹配，则将 `found` 赋值为索引并跳循环。如果 `found >= 0`，则打印“found [item] in position”；否则打印“[item] not found”。列表 4.63 检查匹配项。列表 4.63 你将看到以下输出：

```
found 123 in position 4
```

## 二分查找（迭代法）

二分查找需要排序的数组，并且可以通过迭代算法来实现。如果中间元素小于搜索项，则重复右半部分；如果中间元素大于搜索项，则重复左半部分。

## 二分查找演练

让我们对排序的数字数组进行二分查找演练。

示例 1：`item = 25`，`arr1 = [10,20,25,40,100]`，所以数组的中点是 3。由于 `arr1[3] == item`，算法成功终止。

示例 2：`item = 25`，`arr1 = [1,5,10, 15,20,25,40]`，这意味着中点是 4。第一次迭代：由于 `arr1[4] < item`，我们搜索 `[20,25,40]`。第二次迭代：中间点是 1，对应的值为 25。第三次迭代：25 和数组是单个元素 `[25]`，匹配了项。

示例 3：`item = 25`，`arr1 = [10,20,25,40,100,150]`，所以中点是 4。第一次迭代：由于 `arr1[4] > 25`，我们搜索 `[10,20,25]`。第二次迭代：中间点是 1，对应的值为 20。第三次迭代：25 和数组是单个元素 `[25]`，匹配了项。

示例 4：`item = 25`，`arr1 = [1,5,10, 15,20,30,40]`，所以中点是 4。第一次迭代：由于 `arr1[4] < 25`，我们搜索 `[20,30,40]`。第二次迭代：中间点是 1，对应的值为 30。第三次迭代：25 和数组是单个元素 `[20]`，所以没有匹配项。

## 迭代二分查找代码

列表 4.64 显示了 `binary_search1.sh` 的内容，它演示了如何对数字数组进行二分查找。

```awk
echo "" | awk 'BEGIN {}
```
```
arrl[1] = 1
arrl[2] = 3
arrl[3] = 5
arrl[4] = 123
arrl[5] = 400
found = -1
item = 123
left = 0
right = length(arrl)-1
```
```
printf("array: ")
for(k=1; k<=length(arrl); k++) {
    printf("%d", arrl[k])
}
print("")
```
```
while (left <= right) {
    mid = int(left + (right-left)/2)
    if(arrl[mid] == item) {
        found = mid
        break
    } else if (arrl[mid] < item) {
        left = mid+1
    } else {
        right = mid-1
    }
}
if(found >= 0) {
