### 2.属性标签
* S&emsp;站点&emsp;```${S['活动'].name}```
* SV&emsp;站点变量&emsp;```${SV['活动']['siteUrl']}```
* CS&emsp;当前站点&emsp;```{CS.name}```
* CSV&emsp;当前站点变量&emsp;```${CSV['siteUrl']}```
* C&emsp;栏目&emsp;```${C['00010002'].name}```
* CV&emsp;栏目变量&emsp;```<#assign e =CV[00010002']/>${e['hello']}```
* CC&emsp;当前栏目&emsp;```${CC.name}```
* CCV&emsp;当前栏目变量&emsp;```${CCV['hello']}```
* SS&emsp;站点风格&emsp;```${SS}```

&emsp;**只在内容模块中使用的标签**
* CA&emsp;当前文章&emsp;```${CA.title}```,&emsp;表单字段&emsp;```${CA.fields.表单字段}```
* CAIDX&emsp;当前文章编号&emsp;```${CAIDX}```
* CLIST&emsp;当前文章所在栏目的文章列表&emsp;```<#list CLIST/>```

&emsp;**模块自定义变量**
&emsp;在模块添加的变量，在模块里调用`${var}`，不同的是在模版里挂接模块时候，都需要单独的设置一遍变量值，也就是说更改模块变量值不会改变模版时候所设置的变量值。




