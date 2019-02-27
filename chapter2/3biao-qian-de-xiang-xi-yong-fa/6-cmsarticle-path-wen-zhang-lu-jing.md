6.CMS_ARTICLE_PATH&emsp;文章路径
```
<a href="${CMS_ARTICLE_PATH('${e.id}','${a.id}')}" title="${a.title[0..16]}"  target="_blank">${a.title}</a>
```
也可以用'${e.visitPath}${a.id}.html'
