# 使用说明
## 1.项目中的build添加申明仓库地址：
      maven {
            url "https://raw.githubusercontent.com/akeecai/AndroidResource/master"
        }
## 2.app中的build正常引入需要的相应的包：
      implementation 'com.dayi.base:mwidget:1.1.0'
      implementation 'com.dayi.base:mhttp:1.1.0'
      implementation 'com.dayi.base:mutils:1.1.0'
      implementation 'com.dayi.base:mcommon:1.1.0'
    注意：mcommon库包含了另外三个库，所以如果集成了mcommon就不需要上面三个库了
