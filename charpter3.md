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
