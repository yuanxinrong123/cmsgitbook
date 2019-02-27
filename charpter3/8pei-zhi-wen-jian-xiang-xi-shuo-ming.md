### 8.配置文件详细说明
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
