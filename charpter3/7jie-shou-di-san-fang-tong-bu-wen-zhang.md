### 7.接受第三方同步文章
&emsp;&emsp;CMS 系统提供了数据同步接口。  任何系统都可以遵守CMS数据同步接口协议来发送文章内容。使用场景可以替其他系统发布文章，可以做到快速相应门户显示增加删除相关内容，不用上线下线操作
![](/images/interface.png)
### 同步接口-参数说明
![](/images/interface1.png)
```
xml示例        
接口地址 http://ip:post/cms/info/syncDataArticle.do   参数名称为datexml <infodate>      <!--//cms站点的存储目录  -->      <sitestoredir>mh</sitestoredir>      <!--//操作类型 add增加 update 修改 del 删除  update_1(福建更新策略：先删后插)-->      <optype>update</optype>       <!-- //EDIT = 编辑; APPROVED = 待发布-->      <state>APPROVED</state>       <!-- //栏目id，由cms提供，可以同时同步到不同栏目下，以逗号分割。100000006924,100000006925 -->      <columid>100000006924</columid>       <!-- 文章标题 -->      <title>外部数据接口</title>       <!-- 关键词 -->      <keywords>你好北京海南</keywords>	<!-- 简介 -->      <summary>外部数据接口外部数据接口</summary>      <!-- 来源网站 -->       <outsidesite>www.10010.com</outsidesite>      <!-- 来源的文章id -->      <outsideid>123456789</outsideid>      <!-- 密码：outsidesite + 当前时间XXXX-XX-XX 进行md5加密  加密。注：要保证两个系统的日期一致-->      <pwd>zxcasdqwefdsjljsdlfjiew</pwd>
<!-- 动态表单集合 cname=表单字段名称 type="String/File" 如果是File节点存放的文件路径 http://www.abchina.com/abc.img  节点值是内容：大文本字段要用CDATA括起来 -->	 <fileds>		 <filed cname='f1' type='STRING' >中国</filed>		 <filed cname='f3' type='STRING' >2011-22-11</filed>		 <filed cname='f2' type='STRING' ><![CDATA[如果是大字段内容就包含html符号就用CDATA括起来]]></filed>	         <filed cname='f5' type='FILE' conagreement='SFTP'>/var/www/ppp/abc.xml</filed>         </fileds></infodate>
返回的xml串<result>   <optype>add</optype>   <outsideid>123456789</outsideid>   <res>0/1,2,3,4</res>(0=成功,1=命令不对,2=密码校验失败,3=解析出错,4=其他)   <reszn>成功或者失败原因</reszn></result>      
```

