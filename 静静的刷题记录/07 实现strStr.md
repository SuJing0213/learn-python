# 实现strStr()

给定一个 haystack 字符串和一个 needle 字符串，在 haystack 字符串中找出 needle 字符串出现的第一个位置 (从0开始)。如果不存在，则返回 -1。
**当 needle 是空字符串时，我们应当返回什么值呢?** 这是一个在面试中很好的问题。对于本题而言，当 needle 是空字符串时我们应当返回 0 。这与C语言的 strstr() 以及 Java的 indexOf() 定义相符。

```python
class Solution:
    def strStr(self, haystack: str, needle: str) -> int:
        if needle == "":
            return 0
        if needle not in haystack:
            return -1
        else:
            for index in range(len(haystack)):
                if haystack[index:index+len(needle)] == needle:
                    return index
```

