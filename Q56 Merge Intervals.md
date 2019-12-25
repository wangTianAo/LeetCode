2019.12.25<br>
题中输入的是int[][2],2表示开始和结束两个时间<br>
根据第一个数字，排列2d数组<br>
```java
Arrays.sort(intervals, (a, b) -> a[0] - b[0]);
```
中间只需要逐个比较，如果时间不重叠就直接加到数组中，如果时间有重叠就取start的最小值和end的最大值。<br>

最后输出ArrayList<int[]>转int[][]<br>
```java
result.toArray(new int[result.size()][2])
```
