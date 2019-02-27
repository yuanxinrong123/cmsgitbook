4.CMS_ARTICLE_LIMIT多栏目读取方法</br>
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
