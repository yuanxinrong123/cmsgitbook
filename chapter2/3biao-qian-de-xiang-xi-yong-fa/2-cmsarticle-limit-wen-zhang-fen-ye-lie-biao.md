2.CMS_ARTICLE_LIMIT&emsp;文章分页列表
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
