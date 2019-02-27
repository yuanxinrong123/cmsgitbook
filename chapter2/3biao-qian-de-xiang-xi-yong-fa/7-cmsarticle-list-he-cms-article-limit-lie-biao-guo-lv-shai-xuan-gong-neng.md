7.CMS_ARTICLE_LIST和CMS_ARTICLE_LIMIT列表过滤筛选功能（亮点功能）</br>
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
