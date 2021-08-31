## [实现 strStr()](https://leetcode-cn.com/problems/implement-strstr/) （kmp算法）

实现 strStr() 函数。

给你两个字符串 haystack 和 needle ，请你在 haystack 字符串中找出 needle 字符串出现的第一个位置（下标从 0 开始）。如果不存在，则返回  -1 。

说明：

当 needle 是空字符串时，我们应当返回什么值呢？这是一个在面试中很好的问题。

对于本题而言，当 needle 是空字符串时我们应当返回 0 。这与 C 语言的 strstr() 以及 Java 的 indexOf() 定义相符。

**示例 1：**

```
输入：haystack = "hello", needle = "ll"
输出：2
```

**示例 2：**

```
输入：haystack = "aaaaa", needle = "bba"
输出：-1
```

**示例 3：**

```
输入：haystack = "", needle = ""
输出：0
```





### 双指针

- 匹配串和模式串，用i指针和j指针分别从头开始匹配
- 当匹配相等时，i和j都加1，继续下一个匹配
- 当不相等时，i回到最开始和j匹配到的位置的后面，j回到0，这样为了可以全匹配，比如aaacbb和aac，匹配到i === 2时，他们不相等，这时需要把i移动到第一次匹配成功的后面，就是i - j + 1的位置，再继续和模式串的第一位进行比对

```javascript
var strStr = function (haystack, needle) {
    let i = 0, j = 0
    console.log(123);
    while (i < haystack.length && j < needle.length) {
        if (haystack[i] === needle[j]) {
            j++
            i++
        } else {
            i = i - j + 1
            j = 0
        }

    }
    if(j === needle.length) {
        return i - j
    } else {
        return -1
    }
};
```



优化方案，kmp算法，好吧弄不懂，大概看懂就是，i不动，j动，这样可以减少很多移动次数，而j移动的位置用next数组存着，当匹配不成功的时候，j的下一个位置k放进去next数组里面，