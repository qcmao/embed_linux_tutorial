HTTP协议
========

什么是 HTTP 协议?
-----------------

日常我们使用网络用得最多的无疑是在 Web
浏览器（下文统一使用浏览器）上查找资
料、看视频、看书、看新闻等等，而在浏览器中只需要输入一些搜索就可以得到想要的信
息，这归根于搜索引擎的好处，但是实际上每个网页其实由多个资源组成。我们的浏览器
就是一个 ``HTTP`` 客户端，通过 ``HTTP`` 协议访问服务器，得到服务器中的
HTML 页面、文本
文件、图片、音频等资源，并且将这些资源搬运到浏览器（客户端）
显示给我们。 HTTP 协议是
``Hyper Text Transfer Protocol`` （超文本传输协议）的缩写，
是用于从万维
网 ``（WWW:World Wide Web）`` 服务器传输超文本到本地浏览器的传输协议，它是基于
``TCP/IP`` 协议通信的，因此它也是基于模型运作的，是一个应用层协议，
可以用它来传输服务器的各种资源，如文本、图片、音频等。

HTTP 协议的特点：
-----------------

1. 简单：当客户端向服务器请求服务时，只需传送请求方法和路径即可获取服务器的资源，
   请求方法常用的有 ``GET、 HEAD、 POST`` 等，
   每种方法规定了客户端与服务器通信的类型不同。

2. 快捷： 由于 ``HTTP`` 协议简单，使得 ``HTTP``
   服务器的程序规模小，因而通信速度很快。

3. 灵活： ``HTTP`` 允许传输任意类型的数据对象， 传输的类型由
   ``Content-Type`` 加以标记。

4. 无连接： 无连接的含义是限制每次连接只处理一个请求，
   服务器处理完客户的请求，并收到客户的应答后，即断开连接，简单来说就是每进行一次
   ``HTTP`` 通信，都要断开一次 ``TCP`` 连接， 可随着 ``HTTP``
   的普及，文档中包含大量图片的情况多了起来，每次请求完都要断开 ``TCP``
   连接，无疑增加通信量的开销， 为了解决 ``TCP`` 的连接问题，
   ``HTTP1.1``
   提出了持久连接的方法，即任意一端只要没有明确提出断开连接，则保持
   ``TCP`` 连接状态，这样子就就减少了 ``TCP``
   连接的重复建立和断开所造成的额外开销，减轻了服务端的负载。注意，在
   ``HTTP1.1`` 版本之后才出现持久连接的方法。

5. 无状态： ``HTTP`` 协议是无状态协议，
   无状态是指协议对于事务处理没有记忆能力，即 ``HTTP``
   协议无法根据之前的状态进行本次的请求处理，这就意味着如果后续处理需要前面的信息，它必须重传数据，这样的情况可能导致
   ``HTTP``
   协议传输的数据量增大，当然，凡事都有两面性，在另一方面，在服务器不需要先前信息时它的应答就较快，可以减少服务器的资源消耗，其实这种无状态对于用户来说也是不友好的，因此为了解决无状态的问题，引入了
   ``Cookie``
   技术，这是一种可以让服务器知道用户上一次做了什么操作，并且记录下来，它是存储在客户端之中的，比如我们在淘宝上买东西，我们选择了几个商品，但是到了结账会跳转到另一个页面，此时如果服务器不知道我们选择了哪些商品，那怎么能结账成功呢？
   所以 ``Cookie`` 就是用来绕开 ``HTTP`` 的无状态性的“手段”之一，
   服务器可以设置或读取 ``Cookies``
   中包含信息，让服务器知道我们选择了什么商品，借此维护用户跟服务器会话中的状态，当然，
   ``Cookie`` 会被加密存储在客户端中，直到过期或者手动清除。

URL与资源
---------

我们可以把整个英特网看做是一个巨大的图书馆，里面的资源应有尽有，
并且是对我
们是开放的，我们想要找一本书，那么我们就需要直到他存放在哪里，然后去找到它。
网络中的资源也是应有尽有，那么怎么样才能在网络的海洋中找到我们想要的资源呢？
因此
``URI（Uniform Resource Identifiers）`` 就被设计出来，用于统一管理资源，就像我们去
图书馆找书一样，我们必须通过图书馆的系统，找到书所在的位置，而不是让我们自己一
本一本书去找。

``URL`` 全称是 ``Uniform Resource Locator`` ， 中文叫统一资源定位符，
是互联网上用来标识
某一处资源的绝对地址，使用它我们就必然能找到资源，除非资源已经被转移了。
URI 是 一个通用的概念，由两个子集组成，分别是 ``URL`` 和 ``URN`` ，
``URL`` 是通过资源的位置来标识 资源，而 ``URN``
更高级一点，只需通过资源名字即可识别资源，与他们所处的位置是无关
的，目前暂时还未推广 ``URN`` 。

大部分 URL 都会遵循 ``URL`` 的语法， 一个 ``URL``
的组成有多个不同的组件，一个 ``URL`` 的通用格式如下：

.. code:: html

    <scheme>://<user>:<password>@<host>:<port>/<path>;<params>?<query>#<frag>

当然，绝大部分的 ``URL`` 是不会包含所有组件的内容的，关于 ``URL``
组件具体见表格

+-----------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| 组件            | 描述                                                                                                                                                                                                                                                                                     |
+=================+==========================================================================================================================================================================================================================================================================================+
| 方案 scheme     | 指定访问服务器获取资源时使用哪种协议，有 HTTP、 HTTPS、 FTP、SMTP 等协议。                                                                                                                                                                                                               |
+-----------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| 用户 user       | 某些方案访问资源时候需要指定用户名，才有权限获取资源。                                                                                                                                                                                                                                   |
+-----------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| 密码 password   | 用户名后面可能需要密码进行验证，用户名与密码直接使用“:”冒号分隔连接。                                                                                                                                                                                                                    |
+-----------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| 主机 host       | 资源宿主服务器的主机名或者 IP 地址（点分十进制）。                                                                                                                                                                                                                                       |
+-----------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| 端口 port       | 资源宿主服务器正在监听的端口号，很多方案都有默认的端口号，而无需我们自己填写，比如 HTTP 默认使用 80 端口， HTTPS 默认使用443 端口。 端口不是一个 URL 必须的部分，如果省略端口部分，将采用默认端口。                                                                                      |
+-----------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| 路径 path       | 服务器本地资源的路径，类似于电脑中的文件路径一样，使用“/”将路径与端口隔离。 从域名后的第一个“/”开始到最后一个“/”为止，虚拟目录也不是一个 URL 必须的部分，在路径之后是需要一个文件名，这就是 URL 指定的资源。 文件名部分也不是一个 URL 必须的部分，如果省略该部分，则使用默认的文件名。   |
+-----------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| 参数 params     | 某些方案会使用这个组件来输入参数，可以拥有多个参数，使用“;”符号与路径分隔开。                                                                                                                                                                                                            |
+-----------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| 查询 query      | 某些方案会使用这个组件传递参数以激活应用程序，查询组件的内容，没有通用的格式，用“?”字符与其他组件分隔开                                                                                                                                                                                  |
+-----------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| 片段 frag       | 一小片或者一部分资源的名字，引用对象时，不会将片段组件内容传输给服务器，这个字段是在客户端内部使用的，通过“#”字符与其他组件分隔开。                                                                                                                                                      |
+-----------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

比如像我们论坛的网址： http://www.firebbs.cn/forum.php，它就是一个
``URL`` ，这是最简 单的一个 ``URL``
格式，通过它我们能访问论坛的首页资源， 其中 ``http`` 就是方案，指定
``HTTP`` 协议进行连接 ， 域名就是 ``www.firebbs.cn`` ， ``HTTP``
协议默认端口是 ``80`` ，在这里就无需指定 端口号，路径就是
``forum.php`` ， 其实这个是一个脚本文件，当客户端连接到服务器后， 服务
器会自动运行这个脚本文件， 这样子就访问到我们论坛上的资源了。

HTTP报文
--------

HTTP 报文是由 3 个部分组成，分别是：对报文进行描述的“起始行”，包含属性的
“首部”，以及可选的“数据主体”，对于请求报文与应答报文，只有“起始行”的格式
是不一样的。

请求报文
~~~~~~~~

.. code:: html

    <method> <request-URL> <version>        //起始行
    <headers>                               //首部

    <entity-body>                           //数据主体

应答报文
~~~~~~~~

.. code:: html

    <version> <status> <reason-phrase>        //起始行
    <headers>                               //首部

    <entity-body>                           //数据主体

始行和首部就是由行分隔的 ``ASCII`` 文本组成，
每行都以由两个字符组成的行终止序
列作为结束，其中包括一个回车符 ``（ASCII 码 13）``
和一个换行符 ``（ASCII 码 10）`` ， 这个行 终止序列可以写做 CRLF。

下面就对这两种 ``HTTP`` 报文的各个部分简单描述一下：

-  方法 ``（method）`` ： ``HTTP``
   请求报文的起始行以方法作为开始，方法用来告知服务
   器要做些什么，常见的方法有 ``GET、 POST、 HEAD`` 等，比如
   ``“GET /forum.php HTTP/1.1”`` 使用的就是 ``GET`` 方法。

-  请求 ``URL（request-URL）`` ：指定了所请求的资源。

-  版本 ``（version）`` ：指定报文所使用的 ``HTTP``
   协议版本，其中 ``<major>`` 指定了主要版 本号，
   ``<minor>`` 指定了次要版本号， 它们都是整数，其格式如下：

.. code:: html

    HTTP/<major>.<minor>

-  状态码（status）：这是在 HTTP 应答报文中使用的，
   状态码是在每条响应报文的
   起始行中返回的一个数字码，描述了请求过程中所发送的情况，比如成功、失败
   等，不同的状态码有不同的含义， 具体见表格:

+-------------+------------------+--------------+
| 整体范围    | 已定义使用范围   | 描述         |
+=============+==================+==============+
| 100 ~ 199   | 100 ~ 101        | 信息提示     |
+-------------+------------------+--------------+
| 200~299     | 200 ~ 206        | 成功         |
+-------------+------------------+--------------+
| 300 ~ 399   | 300 ~ 305        | 重定向       |
+-------------+------------------+--------------+
| 400 ~ 499   | 400 ~ 415        | 客户端错误   |
+-------------+------------------+--------------+
| 500 ~ 599   | 500 ~ 505        | 服务器错误   |
+-------------+------------------+--------------+

-  原因短语（reason-phrase）：
   这其实是给我们看的原因短语，因为数字是不够直
   观，它只是状态码的一个文本形式表达而已。

-  首部（header）： HTTP 报文可以有 0 个、 1 个或者多个首部， HTTP
   首部字段向
   请求和响应报文中添加了一些附加信息，从本质上来说，它们是一个 对，
   每个首部都包含一个名字，紧跟着一个冒号“:”，然后是一个可选的空格，
   接着是一个值，最后以 CRLF 结束，比如“Host:
   www.firebbs.cn”就是一个首部。

-  数据主体（entity-body）：这部分包含一个由任意数据组成的数据块，其实这与
   我们前面所讲的报文数据区域是一样的，用于携带数据， HTTP
   报文可以承载很 多类型的数字数据： 图片、视频、音频、 HTML
   文档、软件应用程 序等。


