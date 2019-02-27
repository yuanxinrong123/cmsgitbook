常用方法
数字循环
```
1..5 表示从1到5，原型number..number
对浮点取整数
${123.23?int} 输出123
```
给变量赋值
```
${var?default(“hello world<br>”)?html}如果var is null那么将会被hello world<br>替代
```
判断对象是不是null
```
<#if mouse?exists>
  Mouse found
<#else>
也可以直接${mouse?if_exists})输出布尔形
```
常用格式化日期
```
openingTime必须是Date型,详细查看freemarker文档 Reference->build-in referece->build-in for date
${openingTime?date}
${openingTime?date_time}
${openingTime?time}
```
substring的用法
```
<#assign user=”hello jeen”>
${user[0]}${user[4]}
${user[1..4]}
输出 :
ho
ello  
```
取得字符串的长度
```
var?length
```
大写输出字符
```
var?upper_case
```
小写输出字符
```
var?lower_case
```
首字母大写
```
var?cap_first
```
首字母小写
```
var?uncap_first
```
