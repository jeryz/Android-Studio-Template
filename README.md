#Android Tempplate

###相关文档<br>
[Template Format Document](http://www.i-programmer.info/professional-programmer/resources-and-tools/6845-android-adt-template-format-document.html#toc_escapexmlstring)  +  [FreeMarker](http://freemarker.org/docs/index.html)<br>

###模板介绍<br>
模板存放于studio下的plugins\android\lib\templates<br>
<br>
MyTemplate/ <br>
  * globals.xml     存放全局变量文件<br>
  * recipe.xml      配置引用模板路径和输出文件的路径，及要复制的文件<br>
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

##`<template>`
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

