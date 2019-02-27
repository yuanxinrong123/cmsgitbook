11. 常用方法<br/>
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
去掉字符串前后空格
```
var?trim
```
每个单词的首字符大写
```
var?capitalize
```
类似String.indexof: 
```
"babcdabcd"?index_of("abc") 返回1
"babcdabcd"?index_of("abc",2) 返回5
```
类似String.lastIndexOf
```
last_index_of和String.lastIndexOf类似,同上
```
替换字符串 replace
```
${s?replace(‘ba’, ‘XY’ )}
```
注释标志
```
<#-- 
  这里是注释
-->
```
生成导航
```
<#assign lg = CC.levelCode?length/4>
  <#list 1..lg as x>
    <#assign s=CC.levelCode?substring(0,4*x)>
    <#assign str=str+C[s].name+'-'>
  </#list>
${str}
```
取标题长度
```
<#if nggz.title?length gt 5>${nggz.title[0..5]}<#else>${nggz.title}</#if>
```
根据文章某个字段去读取某个栏目
```
<#assign jlevelcode =CA.fields.对应奖品栏目编号/>
<#assign clevelcode =CA.fields.对应场区栏目编号/>
<#assign huodongid =CA.fields.活动编码/>
<#assign pid =CA.fields.平台编号/>
<#list CMS_ARTICLE_LIST(jlevelcode,5,'AND|活动编码,=,'+huodongid) as a>
```
