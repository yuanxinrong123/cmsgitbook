## 二、CMS模板人员培训
### 1.自定义标签
* CMS_ARTICLE_LIST&emsp;文章列表
* CMS_ARTICLE_LIMIT&emsp;文章分页列表
* CMS_COLUMN_LIST&emsp;栏目列表
* CMS_ARTICLE_PATH&emsp;文章路径
* CMS_DIV_LOAD&emsp;加载静态文件

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
&emsp;在模块添加的变量，在模块里调用${var}，不同的是在模版里挂接模块时候，都需要单独的设置一遍变量值，也就是说更改模块变量值不会改变模版时候所设置的变量值。




### 3.标签的详细用法
1. CMS_ARTICLE_LIST&emsp;文章列表</br>
```
<#assign e = C['00230005']>
  <#list CMS_ARTICLE_LIST('${e.id}',6) as a> 
    <tr><#if a.title?length gt 16>
      <td height="24">
        <a href="${CMS_ARTICLE_PATH('${e.id}','${a.id}')}" title="${a.title[0..16]}"  target="_blank">${a.title}</a>
      </td>
      <#else>
      <td height="24">
        <a href="${CMS_ARTICLE_PATH('${e.id}','${a.id}')}" title="${a.title}"  target="_blank">${a.title}</a> </td>
      </td>
      </#if>
    </tr>
  </#list>    
```
其中，CMS_ARTICLE_LIST('${e.id}',6)也可以写成：</br>
`<#list CMS_ARTICLE_LIST '00010002',6) as a>`指定栏目</br>
`<#list CMS_ARTICLE_LIST '${e.levelcode}',6) as a>` 先声明栏目变量e</br>
`<#list CMS_ARTICLE_LIST '${CC.levelcode}',6) as a>` 当前栏目</br>

2. CMS_ARTICLE_LIMIT文章分页列表
```
<div class="nrong2" id="limitPage">
  <@CMS_ARTICLELIMIT column="${CC.levelCode}" pageDisplay="10" uniqName="uniqName";limitList,page,total,pageCount,pre,next>
    <ul>
      <#list limitList as nggz>
        <li>
          <a href="${CMS_ARTICLE_PATH('${CC.id}','${nggz.id}')}">${nggz.title}</a>
        </li>
      </#list>
    </ul>
</div>
<div class="page">
<table border="0" width="350">
  <tbody>
    <tr>
      <td class="page1" width="50">第&nbsp;<span class="list2_xx">${page}</span>&nbsp;页</td>
      <td class="page1" width="50">共&nbsp;<span class="list2_xx">${pageCount}</span>&nbsp;页&nbsp;&nbsp;</td>
      <td width="50"><a href="#nogo" onclick="$('#limitPage').load('${CC.visitPath}/${ss}uniqName_1.html');"><img src="/images/home.jpg"></a></td>
      <td width="50"><a href="#nogo" onclick="$('#limitPage').load('${CC.visitPath}/${ss}uniqName_${pre}.html');"><img src="/images/last.jpg"></a></td>
      <td width="50"><a href="#nogo" onclick="$('#limitPage').load('${CC.visitPath}/${ss}uniqName_${next}.html');"><img src="/images/next.jpg"></a></td> <td width="50"><a href="#nogo" onclick="$('#limitPage').load('${CC.visitPath}/${ss}uniqName_${pageCount}.html');"><img src="/images/end.jpg" /></a></td>
    </tr>
  </tbody>
</table>
</div>
</@CMS_ARTICLE_LIMIT>
<script>
  $(document).ready(function){
    $("#limitPage").load("${SS}uniqName_1.html")
  }
</script>
```
3. CMS_ARTICLE_LIMTI&emsp;文章分页列表的另一个实现方式（js实现）</br>
使用js的实现方式需要引入实现分页的js文件
```
<script type="text/javascript" src="/js/jquery.pagination.js"></script>
<script type="text/javascript" src="/js/splitPage.js"></script>
```
```
<div  id='limitPage' >
<@CMS_ARTICLE_LIMIT  column="${CC.levelCode}"  pageDisplay="5"  uniqName="uniqName"; limitList,page,total,pageCount,pre,next>
  <div id = "pagination"></div>
  <input type="hidden" id="pageNo" name="pageNo" value="1">
   <script>
    function aaaaa(){
      var pg = document.getElementById("pageNo").value;
      var urlp="${ss}uniqName_"+pg+".html";
      $("#limitPage").load(urlp);
    }
    var funnames="aaaaa();";
    initPagination(${pre+1},${total},5);
   </script>
</@CMS_ARTICLE_LIMIT>
</div>
<script>
  $(document).ready(function(){
     $("#limitPage").load("${SS}uniqName_1.html");
  });
</script>
```
其中：div的id："pagination"不能改变;</br>
input的id:"pageNo"不能改变;</br>
var funnames的名称"funnames"不能改变;</br>
initPagination(${pre+1},${total},5)的三个参数，分别是当前页数，总条数，每页显示条数（要与标签中的pageDisplay的值保持一致，否则显示可能会有问题)。
4. CMS_ARTICLE_LIMIT多栏目读取方法</br>
```
<@CMS_ARTICLE_LIMIT column="00340001,00340002" pageDisplay="10" uniqName="uniqName" currentColumn="${CC.levelCode}" columnSCope="many" order="top_5";limitList,page,total,pageCount,pre,next>
```
在分页某单个栏目下文章，我们还可以使用以前的那样写法
新增的属性有：</br>
1) currentColumn="${CC.levelCode}" 必须要写这句 获得当前栏目</br>
2) columnScope="many"  columnScope="sonson"  columnScope="son"   获取范围 </br>
3) order="top_5" order="level"; 排序方式</br>
其中：当columnScope=many，即栏目可以写多个column="00340001,00340002"可以写多个没有关联的栏目</br>
当columnScope=sonson，即该栏目下所有子孙栏目下面的所有文章，包括本栏目</br>
当columnScope=son，即该栏目下所有儿子栏目下面的所有文章，包括本栏目</br>
当order="level"，即顺序排序在columnScope="many"的时候，按照所写栏目id的顺序排序</br>
当columnScope="sonson"或者"son"的时候按照栏目级别排序，级别高的排在前</br>
当order="top_5",即置顶排序top_num,num代表要置顶显示的个数，例如top_5即为每个栏目下的前5个排在前面，后面的按照栏目的顺序排序</br>
5. CMS_COLUMN_LIST&emsp;栏目列表
```
<#list CMS_COLUMN_LIST('00010001',5) as ccc>
    ${ccc.name}
</#list>
```
6. CMS_ARTICLE_PATH&emsp;文章路径
```
<a href="${CMS_ARTICLE_PATH('${e.id}','${a.id}')}" title="${a.title[0..16]}"  target="_blank">${a.title}</a>
```
也可以用'${e.visitPath}${a.id}.html'
7. CMS_ARTICLE_LIST和CMS_ARTICLE_LIMIT列表过滤筛选功能（亮点功能）</br>
语法：'AND|title,=,你好|内容,like,中国|jiage,>=,2'</br>
AND 是逻辑符号，所有条件是并的关系&&</br>
OR  所有条件是或的关系||</br>
文章基本属性包括 title、summary、keywords 和所对应表单字段</br>
判断符包括：=、`<`、`>`、<=、>=、like；大于小于等是针对于文章字段是数值  类型
例如：
```
 <#list CMS_ARTICLE_LIST(clevelcode,10,'AND|活动编码,=,111000') as a>
 <@CMS_ARTICLE_LIMIT column="${CC.levelCode}" pageDisplay="10" uniqName="uniqName"  where="'AND|活动编码,=,111000'"; limitList, page,total,pageCount,pre,next> 
```
8. CMS_DIV_LOAD（加载静态模块）</br>
用来静态加载栏目下的首页（该标签基于jquery，需要引入相应的js）
特点：
```
${CMS_DIV_LOAD('0010')}	
```
9. 文章，站点，栏目三个对象所拥有的字段，可以在模板中使用
>**（CA）文章包含：**
> id&emsp;文章id
> state &emsp;文章状态
> title&emsp;文章标题
> summary&emsp;文章摘要
> keywords&emsp;文章关键字
> fields&emsp;文章所对应的表单字段
> frticleFields&emsp;把该文章所有的字段值拼接出来
> titleLength&emsp;自动获取长度为40个字符的标题大于40用...表示
**（S）站点包含：**
> name&emsp;网站名称
> storePath&emsp;存储目录
**（C）栏目包含：**
> name&emsp;获得栏目名称
> levelCode&emsp;获得栏目code
> fileDir&emsp;获得栏目存储目录名称
> storeFilePath&emsp;获取栏目存储路径
> visitPath&emsp;获得栏目访问路径
> daoHangPath&emsp;获得栏目导航信息
> parent&emsp;获得父栏目
> articles&emsp;获得已发布和待发布的文章
> listChilds&emsp;获得该栏目的子栏目
10. 语法介绍<br/>
if,else,elseif<br/>
```
<#if x = 1>  x is 1 </#if>
<#if x = 1>  x is 1<#else>  x is not 1 </#if>
```
switch,case,default,break
```
字符串
<#switch being.size>
  <#case "small"> This will be processed if it is small     <#break>
  <#case "medium">     This will be processed if it is medium     <#break>
  <#case "large">     This will be processed if it is large     <#break>
  <#default>     This will be processed if it is neither
</#switch>
数字
<#switch x>
  <#case x = 1>    1
  <#case x = 2>    2
  <#default>    d
</#switch>  
```
list,break<br/>
```
<#assign seq = ["winter", "spring", "summer", "autumn"]>
<#list seq as x>
  ${x_index + 1}. ${x}<#if x_has_next>,</#if>
</#list>
```
list,break<br/>
```
item_index：是list当前值的下标item_has_next：判断list是否还有值
```
assign<br/>
```
生成变量，并且给变量赋值给season赋予序列值
<#assign seasons = ["winter", "spring", "summer", "autumn"]>
给变量test加1<#assign test = test + 1>
```
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
12. 编辑布局的语法
新建布局shi新建布局时用于放入模块的div的编写为：<div class="droppable"></div>
```
<div><!--头部--><div class="bgfff droppable"></div><!--头部--><!--中间--><div class="droppable"></div><!--中间--><!--底部--><div class="droppable"></div><!--底部--></div>
```