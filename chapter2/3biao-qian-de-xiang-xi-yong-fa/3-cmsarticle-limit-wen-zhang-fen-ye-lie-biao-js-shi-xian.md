3.CMS_ARTICLE_LIMIT&emsp;文章分页列表的另一个实现方式（js实现）</br>
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
其中：
* div的id："pagination"不能改变;</br>
* input的id:"pageNo"不能改变;</br>
* var funnames的名称"funnames"不能改变;</br>
* initPagination(${pre+1},${total},5)的三个参数，分别是当前页数，总条数，每页显示条数（要与标签中的pageDisplay的值保持一致，否则显示可能会有问题)。
