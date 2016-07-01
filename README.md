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


