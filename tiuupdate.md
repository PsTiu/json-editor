# 开发备忘
- 开启本地服务，可以测试页面
```
npm run build.nonmin
```
`然后访问 http://127.0.0.1:9001/tests/pages/_demo.html`

- 如果编译代码的是有eslint相关的错误提示，那么可以跑下面命令修复
```
npm run eslint.fix
```


# 已经实现

## 校验字符串是正则表达式
- `"type": "string"`的字段可以通过配置`"isRegex": true`，用于校验输入的字符串是否是正则表达式
- 文案配置可以通过`error_isRegex`字段配置正则表达式书写错误后的提示文字（暂时不支持传参），如：
``` js
"name": {
    "type": "string",
    "description": "First and Last name",
    "minLength": 4,
    "isRegex": true, // 表示字段输入的字符串必须是一个正则表达式
    "default": "Jeremy Dorn"
}
```

## 输入字符串配置了用于校验的正则表达式，支持自定义错误提示语言
- `"type": "string"`的字段如果配置了`"pattern"`字段，那么当输入的值不符合该正则的话，可以通过配置`"patternErrMsg"`字段来用于展示错误提示信息。如：
``` js
 "unit": {
    "type": "string",
    "title": "限频区间单位",
    "description": "设定限频区间的时间长度，如设置QPS，则为1s，如设置1.5分钟内允许请求30次，则此处可填写1m30s",
    "default": "1s",
    "pattern": "(\\d+[smh])+",
    "patternErrMsg":"限频区间单位格式为：整数s（例如13s）或者 整数m整数s（例如1m30s）"  // 如果该字段的值不能匹配pattern字段指定的正则，那么展示这个错误提示
}
```


# 待实现

## 加一些新功能：
- 新开发一套皮肤，参考odp中网关插件的ui样式和交互
- 支持对ui进行分组
- 支持字段开关（和属性checkbox有区别）
    - 如果开关关掉，那么生成的json数据不包含对应的字段
    - json数据初始化ui的时候，如果没有开关对应的字段，也要显示这个字段的ui，此时开关是关的状态


## 对原有功能的优化
- 对现有的`defaults.languages`配置项目做汉化
- 一些写死的文案做可配置汉化
    - 数组copy按钮加上文案配置，目前没有`button_copy_row_title`可以配置，可以参考`button_delete_row_title`