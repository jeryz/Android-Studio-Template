#Android Tempplate

###相关文档<br>
[Template Format Document](http://www.i-programmer.info/professional-programmer/resources-and-tools/6845-android-adt-template-format-document.html#toc_escapexmlstring)  +  [FreeMarker](http://freemarker.org/docs/index.html)<br>

###模板介绍<br>
模板存放在studio安装目录下的plugins\android\lib\templates<br>
一般只需要改template和recipe这两个文件，在template配置要输入的参数，然后编写java，xml模板文件，recipe配置模板文件输出
<br>
Template/ <br>
  * globals.xml     存放全局变量文件<br>
  * recipe.xml      配置从该模板生成代码时应执行的各个指令，如复制文件，配置生成目录等<br>
  * template.xml    配置模板基本信息，输入参数，描述，globals文件和recipe文件<br>
  * template_*.png   模板配图<br>
  * root/ <br>
    * res/ <br>
      * layout <br>
      * values <br>
    * src/ <br>
      * app_package <br>
        * \*.java.ftl   java模板文件<br>
    * AndroidManifest.xml.ftl   manifest模板文件<br>

###`<template>`
```
<template
    format="3"
    revision="1"
    minApi="4"
    minBuildApi="11"
    name="[这个模板的名字]"
    description="[模板的描述]">
    <!--添加support依赖库-->
    <dependency name="[android-support-v4|android-support-v13]" revision="8" />
    <category value="[在模板分类中显示的名字]" />
    
    <parameter
        <!--定义参数id-->
        id="activityName"
        <!--参数显示的名字-->
        name="Activity Name"
        <!--输入参数类型-->
        type="[string|boolean|enum|separator]"
        <!--参数约束条件-->
        constraints="[class|activity|layout|drawable|string|package|id|apilevel|unique|nonempty|exists]"
        <!--根据其他输入的参数来提供建议值-->
        suggest="${layoutToActivity(layoutName)}"
        <!--默认值-->
        default="MainActivity"
        <!--参数的说明-->
        help="The name of the activity class to create." />
    <!-- 参数类型为enum的示例-->
    <parameter
        id="navType"
        name="Navigation Type"
        type="enum"
        default="none">
        <option id="none" default="true">None</option>
        <option id="tabs" minApi="11">Tabs</option>
        <option id="pager" minApi="11">Swipe Views</option>
        <option id="dropdown" minApi="11">Dropdown</option>
    </parameter>
    <!-- 展示模板效果图 -->
    <thumbs>
        <thumb>template_default.png</thumb>
        <thumb navType="tabs">template_tabs.png</thumb>
        <thumb navType="dropdown">template_dropdown.png</thumb>
    </thumbs>
    <!-- 引用全局变量文件 -->
    <globals file="globals.xml.ftl" />
    <!-- 引用输出配置文件 -->
    <execute file="recipe.xml.ftl" />
</template>
```
###globals
```
<globals>
    <global id="activityClass" value="${activityName}Activity" />
</globals>
```
###recipe
```
<recipe>
    <!-- copy 复制文件，默认是root目录下，可配置参数from="原文件路径" to="输出文件路径"-- >
    <copy from="res/drawable-xhdpi" />
    <copy from="res/layout/activity_simple.xml"
                to="res/layout/activity_${activityNameLower}.xml" />
                
    <!-- instantiate 跟copy一样是复制，只不过会自动去掉文件后缀ftl 
    可配置参数from="原文件路径" to="输出文件路径"-- >
    <instantiate from="res/values/strings.xml.ftl" />
    <instantiate from="src/app_package/SimpleActivity.java.ftl"
                       to="${srcOut}/${activityClass}.java" />
   
    <!-- 当创建完成后打开指定的文件 file="文件路径"-->
    <open file="res/layout/${activityNameLower}.xml" />
    
    <!-- <merge> 合并到已有的文件，一般用于合并AndroidManifest.xml，strings.xml等-->
</recipe>
```

###一些模板函数介绍
```
activityToLayout(string) 根据activity名字转换为layout名字
layoutToActivity(string) 根据layout名字转换为activity名字
underscoreToCamelCase(string) 去掉字符串分隔符转驼峰式字符串
camelCaseToUnderscore(string) 转小写单词加分割符<br>
classToResource(string) 剥离class后缀名[Activity|Fragment|Provider|Service]
slashedPackageName(string) 将包名转为路径
extractLetters(string) 去除标点符号和空白字符
escapeXmlString(string)
escapeXmlText(string)
escapeXmlAttribute(string)
```
###一些FreeMarker表达语法
```
<#if 表达式>
  代码
<#else>
  代码
</#if>

<#if 表达式>
  代码
<#else if 表达式>
  代码
</#if>

<#include "*/footer.ftl">

${"string"?ends_with("end")}

${"red"?starts_with("red")}

${GrEeN MoUsE"?lower_case}
```
