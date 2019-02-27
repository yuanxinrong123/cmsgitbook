## 三、开发人员培训
### CMS技术架构图
### Ajax技术
&emsp;&emsp;数据处理等都交给Ajax引擎处理，只有确定需要从服务器读取新数据时再由Ajax引擎代为向服务器提交请求。这样就把一些服务器负担的工作 转嫁到客户端，利用客户端闲置的处理能力来处理，减轻服务器和带宽的负担，从而达到节约ISP的空间及带宽租用成本的目的。

### SSH框架的使用
&emsp;&emsp;SSH为Struts+Spring+Hibernate的组成方式，Struts实现MVC，Spring负责架构的结合，Hibernate进行数据的持久化。通常其分层开发的结构图(以一个业务新增为例)如下：
### 作业调度框架
&emsp;&emsp;Quartz框架的核心是调度器。调度器负责管理Quartz应用运行时环境。调度器不是靠自己做所有的工作，而是依赖框架内一些非常重要的部件。Quartz不仅仅是线程和线程管理。为确保可伸缩性，Quartz采用了基于多线程的架构。启动时，框架初始化一套worker线程，这套线程被调度器用来执行预定的作业。这就是Quartz怎样能并发运行多个作业的原理。Quartz依赖一套松耦合的线程池管理部件来管理线程环境。本片文障中，我们会多次提到线程池管理，但Quartz里面的每个对象是可配置的或者是可定制的。
### JQuery
### HttpClient
### Lucene
### Freemarker
### Memcache
### LRUMAP
### CKEDITOR
### CMS包结构图
### 应用结构图
### 数据库设计图

> 
> CMS_ARTICLE 文章基本表
> CMS_APP  应用程序表
> CMS_ARTICLE_LIMIT  文章约束表
> CMS_PLUGINS 插件管理表
> CMS_COLUMN  栏目表
> CMS_ARTCLE_PIC 文章图片表
> CMS_COLUMN_VAR 栏目变量表
> CMS_ARTCLE_LOG  文章日志表
> CMS_FILED_CLOB 大字段表
> CMS_ARTCLE_VADIO 文章视频表
> CMS_FILED_TEXT 基本字段表
> CMS_PUB_LOG 任务操作记录日志表
> CMS_COLUMN_ARTICLE 栏目文章对应关系表
> CMS_PUB_TASKS  发布任务表
> CMS_FORM_FILED_DEFINE 表单定义表
> CMS_PD         流程表
> CMS_RESOURCE   资源表
> CMS_ROLE_COLUMN_AUTH  角色对应栏目数据权限表
> CMS_ROLE       角色表
> CMS_PUB_DETAIL_LOG 任务操作详细表
> CMS_FUNC 功能表
> CMS_LAYOUT  布局定义表
> CMS_COLUMN_TEMPLATE_VAR_VALUE 栏目模板变量设置表
> CMS_SITE 站点CMS_COLUMN_TEMPLATES 栏目模板表
> CMS_TEMPLATE_MODULES 模版模块关联关系配置表
> CMS_MODULE 模块
> CMS_TEMPLATE_MODULE_VAR 模版变量设置表
> CMS_MODULE_VAR 模块变量
> CMS_SITE_CONFIG 站点信息配置表
> CMS_TEMPLATE_DEF 模版定义表
> CMS_SITE_VAR 站点变量
> CMS_FAVORITE_MENU 用户常用应用
> CMS_PLUGIN_EYE_ADS 点睛广告管理
> CMS_FORM 表单
> CMS_ROLE_FUNC_AUTH 角色功能关联表
> CMS_PLUGIN_COMMENT 评论管理
> CMS_SITE_STYLE站点风格表

### 接入BMS系统
&emsp;&emsp;CMS 系统可接入权限管理系统（BMS）。 通过权限系统传过来的用户。来判断是否存在，不存在自动创建，可根据传过来的权限来自动创建cms系统相应的角色。

### 同步接口-参数说明

```
xml示例        
接口地址 http://ip:post/cms/info/syncDataArticle.do   参数名称为datexml <infodate>      <!--//cms站点的存储目录  -->      <sitestoredir>mh</sitestoredir>      <!--//操作类型 add增加 update 修改 del 删除  update_1(福建更新策略：先删后插)-->      <optype>update</optype>       <!-- //EDIT = 编辑; APPROVED = 待发布-->      <state>APPROVED</state>       <!-- //栏目id，由cms提供，可以同时同步到不同栏目下，以逗号分割。100000006924,100000006925 -->      <columid>100000006924</columid>       <!-- 文章标题 -->      <title>外部数据接口</title>       <!-- 关键词 -->      <keywords>你好北京海南</keywords>	<!-- 简介 -->      <summary>外部数据接口外部数据接口</summary>      <!-- 来源网站 -->       <outsidesite>www.10010.com</outsidesite>      <!-- 来源的文章id -->      <outsideid>123456789</outsideid>      <!-- 密码：outsidesite + 当前时间XXXX-XX-XX 进行md5加密  加密。注：要保证两个系统的日期一致-->      <pwd>zxcasdqwefdsjljsdlfjiew</pwd>
<!-- 动态表单集合 cname=表单字段名称 type="String/File" 如果是File节点存放的文件路径 http://www.abchina.com/abc.img  节点值是内容：大文本字段要用CDATA括起来 -->	 <fileds>		 <filed cname='f1' type='STRING' >中国</filed>		 <filed cname='f3' type='STRING' >2011-22-11</filed>		 <filed cname='f2' type='STRING' ><![CDATA[如果是大字段内容就包含html符号就用CDATA括起来]]></filed>	         <filed cname='f5' type='FILE' conagreement='SFTP'>/var/www/ppp/abc.xml</filed>         </fileds></infodate>
返回的xml串<result>   <optype>add</optype>   <outsideid>123456789</outsideid>   <res>0/1,2,3,4</res>(0=成功,1=命令不对,2=密码校验失败,3=解析出错,4=其他)   <reszn>成功或者失败原因</reszn></result>      
```

### 配置文件详细说明
```
1.searchengine.properties（重要参数修改） #<!--memcache开关配置 true使用memcache  false不使用memcache-->           memcacheswitch=false#<!--文章预览方式配置-->         #apachePath=http\://localhost\:8080#<!--同步数据ip限制 xx.xx.xx.xx;yy.yy.yy.yy;pp.pp.pp.pp-->              ipcheck=192.168.2.5;127.0.0.1;192.168.2.61;192.168.1.26;192.168.1.52#<!--同步数据站点附件存放文件夹-->              localpath=_upload
```
```
2. memcachedb.xml     如果用memcachedb则需要配置该文件内容
```
```
3. city.properties      该文件是配置“复制创建栏目”省市对应配置
```
```
4. jdbc.properties      配置数据库地址
```
```
5. log4j.xml      配置日志打印方式及位置
```
### 部署升级注意点
> 
 1如果是迁移CMS要修改站点表的备份路径 2.如果数据库导入的是dmp数据包。表空间要一致 3.cms提供已做好例子。可以导入（表空间为CMSNEW）        Imp xxxx/xxx@xxxx file= zhongguoyidongcms.dmp fromuser=cmstest touser=xxxx        复制解压tymh2012.rar到ROOT下4. Cms5部署在weblogc11平台下需要注意点         把WEB-INF\lib\xalan-2.5.1.jar  删掉   Cms5部署在weblogc9平台下学要注意         把weblogic_9.xml 改称weblogic.xmlCms5部署在weblogc10平台下学要注意          mv xml-apis-2.0.2.jar xml-apis-2.0.2.jar.bak
在新创建模版和新增栏目等操作，方式为环境连接正式库最为方便

### 用户名 superman 密码 superman