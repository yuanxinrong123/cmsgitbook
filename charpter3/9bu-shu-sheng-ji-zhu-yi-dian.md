### 9.部署升级注意点

1.如果是迁移CMS要修改站点表的备份路径 
2.如果数据库导入的是dmp数据包。表空间要一致 
3.cms提供已做好例子。可以导入（表空间为CMSNEW）
Imp xxxx/xxx@xxxx file= zhongguoyidongcms.dmp fromuser=cmstest touser=xxxx
复制解压tymh2012.rar到ROOT下
4. 
* Cms5部署在weblogc11平台下需要注意点  
把WEB-INF\lib\xalan-2.5.1.jar  删掉   
* Cms5部署在weblogc9平台下学要注意         把weblogic_9.xml 改称weblogic.xml
* Cms5部署在weblogc10平台下学要注意          mv xml-apis-2.0.2.jar xml-apis-2.0.2.jar.bak
在新创建模版和新增栏目等操作，方式为环境连接正式库最为方便

