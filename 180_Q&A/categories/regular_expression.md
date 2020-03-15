# Python正则表达式

### 88.使用正则表达式匹配出<html><h1>张明 98 分</html>中的地址 a="张明 98 分"，用 re.sub，将 98 替换为 100
```python
import re
s = '<html><h1>张明 98 分</html>'
res = re.sub(r'\d{2,}', '100', s)
```


### 89.正则表达式匹配中(.*)和(.*?)匹配区别？
**解析正则表达式`r'(.*) are (.*?) .*'`就知道了。
1. `r`表示raw字符串，忽略字符串中的转义字符，这个pattern中没有反斜杠，所以前面的`r`可有可无；
2. `(.*)`：为第一个匹配分组，匹配除换行符之外的所有字符，贪婪匹配，匹配尽可能多的字符；
3. `(.*?)`：为第二个匹配分组，`*, +, {m, n}`后面加了一个`?`之后变成非贪婪模式，只匹配一个；
4. 最后的`.*`没有加括号，匹配结果不计入分组中；
5. match_group.group()等同于match_group.group(0)，为所有匹配分组；group(1)、group(2)...分别匹配第1、2...个分组。
6. `re.M`：多行匹配，影响 ^ 和 $；`re.I`：使匹配对大小写不敏感。

```python
import re
line = "The cats are smarter than dogs"
matchObj = re.match( r'(.*) are (.*?) .*', line, re.M|re.I)
print(matchObj.group(1))
print(matchObj.group(2))
```
输出：
```python
The cats
smarter
```

### 90.写一段匹配邮箱的正则表达式
```python
r'^[0-9a-zA-Z_]{0, 19}@[0-9a-zA-Z]{1,13}\.[com,cn,net]{1,3}$'
```