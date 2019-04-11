# 修改setter模板
>ait + insert 调出getter/setter自动生成页面，点击右侧的 ... 按钮，新增template，   
>实现 String 添加 trima() 效果

```Java
#set($paramName = $helper.getParamName($field, $project))
#if($field.modifierStatic)
static ##
#end
void set$StringUtil.capitalizeWithJavaBeanConvention($StringUtil.sanitizeJavaIdentifier($helper.getPropertyName($field, $project)))($field.type $paramName) {
#if ($field.name == $paramName)
    #if (!$field.modifierStatic)
    this.##
    #else
        $classname.##
    #end
#end
$field.name = ##
#if($field.string)
    $paramName == null ? null : $paramName.##
trim();
#else
    $paramName;
#end
}
```
