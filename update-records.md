## RedirectTools

2020.10.18:

+ 经过考虑之后去除代理的功能
+ 功能后续应该不会再增加，会逐渐优化页面效果和操作流程
+ 更新版本为1.3.2

2020.09.08:

- 更新了原网址的匹配方式
- 优先匹配以输入的原网址内容开始的网址
- 匹配不成功之后使用正则匹配
- 正则匹配需要注意，因为是字符串转过去，所以如果需要自己手动将转义字符进行转义 \\ -> \\\\
- 版本更新为1.3.1

2020.09.07:

- 重构代码风格为面向对象，易于阅读和修改
- 目前为全局静态类的风格，类之间有相互调用
- 旧的js文件保留为xxx-old.js，留作备用
- 暂时删除右键设置代理，后期可能会添加回来，需要规范化
- 版本更新为1.3.0

2020.08.23:

- 版本更新为1.2.0，软件重命名为RedirectTools

- 新增代理选择框，全局代理开关（代理旁边的选择框，选中即为全局代理，否则为gfw模式）

- 更新通过链接增加代理（建议自己在编写时加上一个无代理的代理，proxyUrl为noproxy即可）

  - ```json
    {
      "proxies":[
        {
          "name":"noProxy",
          "proxyUrl":"noproxy"
        },
        {
          "name":"local1080",
          "proxyUrl":"PROXY 127.0.0.1:1080"
        }
      ]
    }
    ```

2020.08.12：

- 考虑到json格式的大批量数据，所以增加了网址格式。
- 使用方法，填写规则时，在重定向的地方以**jsonf:**开头，后面跟上返回json格式内容的网址。

2020.08.11：

- 重定向存在跨域问题，所以实际上并不能很好地实现替换返回值。

- 增加修改返回数据，目前支持json数据，原理为将用户输入的数据经过编码作为 data:-URL 进行重定向使用。

- 使用方法，填写规则时，在重定向的地方以**json:**开头，后面跟上json格式的数据即可。

- 增加js文件替换支持，原理同上，不过是在添加规则之后异步加载在变量里，在拦截时调用变量里面的数据。

- 使用方法，填写规则时，在重定向的地方以**js:**开头，后面跟上替换之后的js文件网址。

  chrome修改返回数据思路参考：https://www.cnblogs.com/h2zZhou/p/9235152.html

2020.08.09：

- 新增通过链接添加规则。

- 可以自己写一个文件上传到服务器，只要返回的数据格式满足给出的标准，就可以添加成功。

  - ```   json
    {
        "allRule":[
            {
                "url":"https://www.google.com/",
                "reUrl":"https://www.baidu.com/",
                "switch":"checked"
            },{
                "url":"https://www.youtube.com/",
                "reUrl":"https://www.baidu.com/",
                "switch":"checked"
            }
        ]
    }
    ```

+ url 为被重定向的网址，reUrl为重定向之后的网址，switch有两个值，checked表示开启规则，unchecked表示不开启规则。

2020.07.31：

- 新增设置代理功能，在任意页面右键，在[WebSiteRedirect]菜单下会有设置代理和取消代理。
- 代理形式：schema host/ip:port 示例：HTTP 127.0.0.1:1080
-  目前默认为输入协议下的全局代理，暂不支持自定义代理。

2020.07.30：

- 新增右键菜单 [将当前页添加到规则]，在任意页面右键，点击之后会把当前页面的网址作为原网址添加规则，点击之后会有弹框输入重定向后的网址。
- 版本号更改为1.0.0。
- 当前版本作为第一个正式版。

2020.07.29：

- 新增了全局User-Agent切换，目前不支持自定义，目前内置chrome、Firefox、IPhone、Android。
- 界面布局用表格简单优化了一下。

2020.07.27：

- 更新了规则格式，新增switch属性，用于判断当前规则是否开启。
- popup页面新增复选框，选中为开启规则，不选中为关闭规则。
- 版本号更改为0.0.2。

--------

1. 起因

   因为有用到网址重定向的需要，主要是用于替换某些指定的JS，实现某些特定的功能。最先开始是使用Gooreplacer，这也是一个Chrome插件，功能其实比我现在要实现的功能要多。但是我希望可以自己完成一个插件，自己进行定制化的修改。

2. 功能

   这个项目是一个用于网址重定向的Chrome插件，可以在点击插件图标时弹出设置页面（popup页面），此页面显示当前现存的规则，可以进行增、删、改、清空。

3. 使用说明

   将代码下载下来，然后解压到一个文件夹，在chrome扩展的开发者模式下-》加载解压缩的扩展。

4. 后续开发

   - 匹配规则

     目前的匹配是根据网址字符串是否相等进行判断的，后续希望可以添加正则匹配和重定向开关。

   + 美化

     插件的界面没有美化，我也不是很感冒，所以如果有大佬的话，希望可以帮忙修改下，谢谢。

   + 规则库

     我希望可以建一个在线规则库，在软件中增加根据链接批量添加规则。

   + 规则同步

     目前代码中使用的是chrome.storage.sync，官方文档是说可以根据chrome账号进行同步，后续希望可以自己构建同步机制。

   + 分享

     后期可以通过使用链接批量添加的功能实现分享功能。

PS.我也是从零开始，对着文章写的这个插件，如果有小伙伴一起玩就更好了，我这里附上我学习的编写插件的文章。

Chrome插件开发攻略：https://www.cnblogs.com/liuxianan/p/chrome-plugin-develop.html

chrome.webRequest：https://www.cnblogs.com/h2zZhou/p/9238251.html