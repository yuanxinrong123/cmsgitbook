9.文章，站点，栏目三个对象所拥有的字段，可以在模板中使用
**（CA）文章包含：**
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
