10.语法介绍<br/>
if,else,elseif<br/>
```
<#if x = 1>  x is 1 </#if>
<#if x = 1>  x is 1<#else>  x is not 1 </#if>
```
switch,case,default,break
```
字符串
<#switch being.size>
  <#case "small"> This will be processed if it is small     <#break>
  <#case "medium">     This will be processed if it is medium     <#break>
  <#case "large">     This will be processed if it is large     <#break>
  <#default>     This will be processed if it is neither
</#switch>
数字
<#switch x>
  <#case x = 1>    1
  <#case x = 2>    2
  <#default>    d
</#switch>  
```
list,break<br/>
```
<#assign seq = ["winter", "spring", "summer", "autumn"]>
<#list seq as x>
  ${x_index + 1}. ${x}<#if x_has_next>,</#if>
</#list>
```
list,break<br/>
```
item_index：是list当前值的下标item_has_next：判断list是否还有值
```
assign<br/>
```
生成变量，并且给变量赋值给season赋予序列值
<#assign seasons = ["winter", "spring", "summer", "autumn"]>
给变量test加1<#assign test = test + 1>
```
