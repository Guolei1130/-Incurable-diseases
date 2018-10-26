### WebView goback问题。

https://www.zhihu.com/question/40943177

目标结果。goback不刷新。

#### 尝试方案1

每次都新建WebView。这种方案很不成熟。但考虑到某些单页应用。暂时可用。


### evaluateJavascript返回值问题

* 需要用apache的[StringEscapeUtils.java](https://github.com/apache/commons-lang/blob/master/src/main/java/org/apache/commons/lang3/StringEscapeUtils.java)对json进行反转义。

* 返回值会对string再加""，而因此一些转义。