1.CMS_ARTICLE_LIST&emsp;文章列表</br>
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
其中，CMS_ARTICLE_LIST('${e.id}',6)也可以写成：
`<#list CMS_ARTICLE_LIST '00010002',6) as a>`指定栏目
`<#list CMS_ARTICLE_LIST '${e.levelcode}',6) as a>` 先声明栏目变量e
`<#list CMS_ARTICLE_LIST '${CC.levelcode}',6) as a>` 当前栏目

