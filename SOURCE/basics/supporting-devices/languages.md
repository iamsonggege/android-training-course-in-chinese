> 编写: [Lin-H](http://github.com/Lin-H) - 校对:

> 原文: <http://developer.android.com/training/basics/supporting-devices/languages.html>

# 适配不同的语言

把UI中的字符串存储在外部文件，通过代码提取，总是一种很好的做法。Android可以通过工程中的资源目录轻松实现这一功能。

如果你使用Android SDK Tools(详见[Creating an Android Project](https://developer.android.com/training/basics/firstapp/creating-project.html))来创建工程，则在工程的根目录会创建一个`res/`的目录，目录中包含所有资源类型的子目录。其中包含工程的默认文件比如`res/values/strings.xml`，用来保存你的字符串值。

## 创建区域设置目录和字符串文件

为了支持多国语言，在`res/`中创建一个额外的`values`目录以连字符和ISO国家代码结尾命名，比如`values-es/` 是包含简单的区域资源，语言代码为"es"的区域设置目录。Android会在运行时根据设备的区域设置，加载相应的资源。

若你决定支持某种语言，则需要创建资源子目录和字符串资源文件，例如:

```
MyProject/
    res/
       values/
           strings.xml
       values-es/
           strings.xml
       values-fr/
           strings.xml
```

添加不同区域语言的字符串值到相应的文件。

在运行时，Android系统会根据用户设备当前的区域设置，使用相应的字符串资源。

例如 下面列举了几个不同语言对应不同的字符串资源文件。

英语(默认区域语言)，`/values/strings.xml`:

```xml
<?xml version="1.0" encoding="utf-8"?>
<resources>
    <string name="title">My Application</string>
    <string name="hello_world">Hello World!</string>
</resources>
```

西班牙语，`/values-es/strings.xml`:

```xml
<?xml version="1.0" encoding="utf-8"?>
<resources>
    <string name="title">Mi Aplicación</string>
    <string name="hello_world">Hola Mundo!</string>
</resources>
```

法语，`/values-fr/strings.xml`:

```xml
<?xml version="1.0" encoding="utf-8"?>
<resources>
    <string name="title">Mon Application</string>
    <string name="hello_world">Bonjour le monde !</string>
</resources>
```

>**Note**：你可以在任何资源类型中使用区域修饰词(或者任何配置修饰符)，比如给bitmap提供本地化的版本，更多信息见[Localization](https://developer.android.com/guide/topics/resources/localization.html)。

## 使用字符资源

你可以在你的源代码和其他XML文件中，通过`<string>`元素的`name`属性来引用你的字符串资源。

在你的源代码中你可以通过`R.string.<string_name>`语法来引用一个字符串资源，很多方法都可以通过这种方式来接受字符串。

例如:

```java
// 从你的 app's 资源中获取一个字符串资源
String hello = getResources().getString(R.string.hello_world);

// 或者提供给一个需要字符串作为参数的方法
TextView textView = new TextView(this);
textView.setText(R.string.hello_world);
```

在其他XML文件中，每当XML属性要接受一个字符串值时，你都可以通过`@string/<string_name>`语法来引用字符串资源。

例如:

```xml
<TextView
    android:layout_width="wrap_content"
    android:layout_height="wrap_content"
    android:text="@string/hello_world" />
```
