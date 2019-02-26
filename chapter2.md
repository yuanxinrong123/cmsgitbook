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
