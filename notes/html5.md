# html5标签

## 文本标签
### p
* ``<p>``标签是一个块级标签

### br,wbr
* ``<br>``标签换行，``<wbr>``则是可告诉浏览器在页面宽度不足时在哪换行
* **注意**，块级元素的间隔不要使用``<br>``来产生，而是要使用css来指定

### hr
*  通常用来分割两个不同的主题，这就是一个水平线

### pre
* 保留标签内部原始的换行和空格
* html标签在``<pre>``内部还是起作用的，``<pre>``只会保留空格和换行，不会保留html标签。



## 列表标签
* **<ol>**
    * ``<ol>``标签是一个有序列表容器（ordered list），会在内部的列表项前面产生数字编号。列表项的顺序有意义时，比如排名，就会采用这个标签。



## 图像标签
### img
* ``<img>``默认是一个行内元素，与前后的文字处在同一行。
    * 如果图片很大，又与文字处在同一行，那么图片将把当前行的行高撑高，并且图片的底边与文字的底边在同一条水平线上。
    * ``<img>``可以放在``<a>``标签内部，使得图片变成一个可以点击的链接。
    * 以下为该元素的属性
        * （1）**alt 属性**
                    alt属性用来设定图片的文字说明。图片不显示时（比如下载失败，或用户关闭图片加载），图片的位置上会显示该文本。

        * （2）**width 属性**，**height 属性** 
                    1、图片默认以原始大小插入网页，width属性和height属性可以指定图片显示时的宽度和高度，单位是像素或百分比。
                    2、注意，一旦设置了这两个属性，浏览器会在网页中预先留出这个大小的空间，不管图片有没有加载成功。不过，由于图片的显示大小可以用 CSS 设置，所以不建议使用这两个属性。
                    3、一种特殊情况是，width属性和height属性只设置了一个，另一个没有设置。这时，浏览器会根据图片的原始大小，自动设置对应比例的图片宽度或高度。

        * （3）**srcset**，**sizes**
                    srcset属性用来指定多张图像，适应不同像素密度的屏幕。它的值是一个逗号分隔的字符串，每个部分都是一张图像的 URL，后面接一个空格，然后是像素密度的描述符。请看下面的例子。<img srcset="foo-320w.jpg,foo-480w.jpg 1.5x,foo-640w.jpg 2x" src="foo-640w.jpg">
                    如果srcset属性都不满足条件，那么就加载src属性指定的默认图像。

        * （4）**referrerpolicy** 
                    <img>导致的图片加载的 HTTP 请求，默认会带有Referer的头信息。referrerpolicy属性对这个行为进行设置。

        * （5）**crossorigin**
                    有时，图片和网页属于不同的网站，网页加载图片就会导致跨域请求，对方服务器可能要求跨域认证。crossorigin属性用来告诉浏览器，是否采用跨域的形式下载图片，默认是不采用。
                    简单说，只要打开了这个属性，HTTP 请求的头信息里面，就会加入origin字段，给出请求发出的域名，不打开这个属性就不加。
                    一旦打开该属性，它可以设为两个值。
                    anonymous：跨域请求不带有用户凭证（通常是 Cookie）。
                    se-credentials：跨域请求带有用户凭证。

        * （6）**loading**
                    loading属性可以取以下三个值:
                    auto：浏览器默认行为，等同于不使用loading属性。
                    lazy：启用懒加载。
                    eager：立即加载资源，无论它在页面上的哪个位置。

### figure，figcaption
* ``<figure>``标签可以理解为一个图像区块，将图像和相关信息封装在一起。``<figcaption>``是它的可选子元素，表示图像的文本描述，通常用于放置标题，可以出现多个。
    * 除了图像，``<figure>``还可以封装引言、代码、诗歌等等。它等于是一个将主体内容与附加信息，封装在一起的语义容器。
### srcset，sizes
* srcset属性用来指定多张图像，适应不同像素密度的屏幕。它的值是一个逗号分隔的字符串，每个部分都是一张图像的 URL，后面接一个空格，然后是像素密度的描述符。请看下面的例子。
  
    ```html
    <img srcset="foo-320w.jpg,
    foo-480w.jpg 1.5x,
    foo-640w.jpg 2x" 
    src="foo-640w.jpg">
    ```

    * 如果srcset属性都不满足条件，那么就加载src属性指定的默认图像。

    * 像素密度的适配，只适合显示区域一样大小的图像。如果希望不同尺寸的屏幕，显示不同大小的图像，srcset属性就不够用了，必须搭配sizes属性。
    ```html
    <img srcset="foo-160.jpg 160w,
             foo-320.jpg 320w,
             foo-640.jpg 640w,
             foo-1280.jpg 1280w"
     sizes="(max-width: 440px) 100vw,
            (max-width: 900px) 33vw,
            254px"
     src="foo-1280.jpg">
    ```

     * 宽度描述符就是图像原始的宽度，加上字符w。上例的四种图片的原始宽度分别为160像素、320像素、640像素和1280像素。

     * 上面代码中，sizes属性给出了三种屏幕条件，以及对应的图像显示宽度。宽度不超过440像素的设备，图像显示宽度为100%；宽度441像素到900像素的设备，图像显示宽度为33%；宽度900像素以上的设备，图像显示宽度为254px。

     * 浏览器根据当前设备的宽度，从sizes属性获得图像的显示宽度，然后从srcset属性找出最接近该宽度的图像，进行加载。假定当前设备的屏幕宽度是480px，浏览器从sizes属性查询得到，图片的显示宽度是33vw（即33%），等于160px。srcset属性里面，正好有宽度等于160px的图片，于是加载foo-160.jpg。

### picture
* ``<img>``标签的srcset属性和sizes属性分别解决了像素密度和屏幕大小的适配
    * 但如果要同时适配不同像素密度、不同大小的屏幕，就要用到``<picture>``标签
    * ``<picture>``是一个容器标签，内部使用``<source>``和``<img>``，指定不同情况下加载的图像。
* ``<picture>``内部的``<source>``标签，主要使用media属性和srcset属性。
    * media属性给出媒体查询表达式，srcset属性就是``<img>``标签的srcset属性，给出加载的图像文件。
    * sizes属性其实这里也可以用，但由于有了media属性，就没有必要了。
    * 浏览器按照``<source>``标签出现的顺序，依次判断当前设备是否满足media属性的媒体查询表达式，如果满足就加载srcset属性指定的图片文件，并且不再执行后面的``<source>``标签和``<img>``标签。
    * ``<img>``标签是默认情况下加载的图像，用来满足上面所有``<source>``都不匹配的情况，或者不支持``<picture>``的老式浏览器。
* 除了响应式图像，``<picture>``标签还可以用来选择不同格式的图像。比如，如果当前浏览器支持 Webp 格式，就加载这种格式的图像，否则加载 PNG 图像。
```html
    <picture>
    <source type="image/svg+xml" srcset="logo.xml">
    <source type="image/webp" srcset="logo.webp"> 
    <img src="logo.png" alt="ACME Corp">
    </picture>
```



## 链接标签
### a 

* href
    * href属性给出链接指向的网址。它的值应该是一个 URL 或者锚点。锚点是连接内#后加元素id

> ps : href属性在使用的时候一定不要来留空，若暂时不需要写地址则尽量用#和JavaScript：；。若直接留空会刷新页面

* **href与src的区别**

    * href(hypertext reference)指超文本引用，表示当前页面引用了别处的内容

    * src(source)表示来源地址，表示把别处的内容引入到当前页面

    * 所以<img>、<script>、<iframe>等应该使用src，而<a>和<map>应该使用href

* hreflang
    * hreflang属性给出链接指向的网址所使用的语言，纯粹是提示性的，没有实际功能
        ```html
        <a
            href="https://www.example.com"
            hreflang="en"
            >示例网址</a>
        ```

* title

    * title属性给出链接的说明信息。鼠标悬停在链接上方时，浏览器会将这个属性的值，以提示块的形式显示出来

* target
    * target属性指定如何展示打开的链接。它可以是在指定的窗口打开，也可以在<iframe>里面打开。
    * target属性的值也可以是以下四个关键字之一。
        * self：当前窗口打开，这是默认值。
        * blank：新窗口打开。
        * parent：上层窗口打开，这通常用于从父窗口打开的子窗口，或者<iframe>里面的链接。如果当前窗口没有上层窗口，这个值等同于_self。
        * top：顶层窗口打开。如果当前窗口就是顶层窗口，这个值等同于_self
    
* 使用target属性的时候，最好跟rel="noreferrer"一起使用，这样可以避免安全风险。
  
* target的属性值也可以直接给定，这样如果没有你给定名字的新窗口，就会创建一个以target里的值为名字的新窗口
  
* rel
    * rel属性说明链接与当前页面的关系。
    * 下面是一些常见的rel属性的值。
        * alternate：当前文档的另一种形式，比如翻译。
        * author：作者链接。
        * bookmark：用作书签的永久地址。
        * external：当前文档的外部参考文档。
        * help：帮助链接。
        * license：许可证链接。
        * next：系列文档的下一篇。
        * nofollow：告诉搜索引擎忽略该链接，主要用于用户提交的内容，防止有人企图通过添加链接，提高该链接的搜索排名。
        * noreferrer：告诉浏览器打开链接时，不要将当前网址作为 HTTP 头信息的Referer字段发送出去，这样可以隐藏点击的来源。
        * noopener：告诉浏览器打开链接时，不让链接窗口通过 JavaScript 的window.opener属性引用原始窗口，这样就提高了安全性。
        * prev：系列文档的上一篇。
        * search：文档的搜索链接。
        * tag：文档的标签链接。
    
* referrerpolicy
  
    * referrerpolicy属于用于精确设定点击链接时，浏览器发送HTTP头信息的referer字段的行为。
    
* 该属性可以取下面八个值：no-referrer、no-referrer-when-downgrade、origin、origin-when-cross-origin、unsafe-url、same-origin、strict-origin、strict-origin-when-cross-origin。
  
    * 其中，no-referrer表示不发送Referer字段，same-origin表示同源时才发送Referer字段，origin表示只发送源信息（协议+域名+端口）。其他几项的解释，请查阅 HTTP 文档。

* ping
    * ping属性指定一个网址，用户点击时，会向该网址发出一个post请求，通常用于跟踪用户的行为。
    
* type
  
    * type属性给出链接url的MIME类型，比如到底是网页，还是图像或文件。它也是纯粹提示性的属性，没有实际功能。
* download
    * download属性表明当前链接用于下载，而不是跳转到另一个url
    * download只在链接与网页同源的时，才会生效。也就是说，链接应该与网址属于同一个网站
    ```html
    <a href="demo.txt" download>下载</a>
    ```
    * 如果download属性设置了值，那么这个值就是下载的文件名若不设置值的话就以链接的值为属性名。
    * 如果链接点击后，服务器的 HTTP 回应的头信息设置了Content-Disposition字段，并且该字段的值与download属性不一致，那么该字段优先，下载时将显示其设置的文件名。
    * download属性还有一个用途，就是有些地址不是真实网址，而是数据网址，比如data:开头的网址。这时，download属性可以为虚拟网址指定下载的文件名。
    ```html
    <a href="data:,Hello%2C%20World!" download="hello.txt">点击</a>
    ```
    链接点击后，下载的hello.txt文件内容就是“Hello, World!”。
* 邮件链接
    * 链接也可以指向一个邮件地址，使用**mailto**协议。用户点击后，浏览器会打开本机默认的邮件程序，让用户向指定的地址发送邮件。
    ```html
    <a href="mailto:contact@example.com">联系我们</a>
    ```
    * 上面代码中，链接就指向邮件地址。点击后，浏览器会打开一个邮件地址，让你可以向contact@example.com发送邮件。
    * 除了邮箱，邮件协议还允许指定其他几个邮件要素。
        * subject：主题
        * cc：抄送
        * bcc：密送
        * body：邮件内容
    * 使用方法是将这些邮件要素，以查询字符串的方式，附加在邮箱地址后面。
    ```html
    <a href="mailto:foo@bar.com?cc=test@test.com&subject=The%20subject&body=The%20body">发送邮件</a>
    ```
    * 上面代码中，邮件链接里面不仅包含了邮箱地址，还包含了cc、subject、body等邮件要素。这些要素的值需要经过 URL 转义，比如空格转成%20。
    * 不指定邮箱也是允许的，就像下面这样。这时用户自己在邮件程序里面，填写想要发送的邮箱，通常用于邮件分享网页。```<a href="mailto:">告诉朋友</a>```
* 电话链接
  
    * 如果是手机浏览的页面，还可以使用tel协议，创建电话链接。用户点击该链接，会唤起电话，可以进行拨号。
```html
    <a href="tel:13312345678">13312345678</a>
```
    * 上面代码在手机中，点击链接会唤起拨号界面，可以直接拨打指定号码。

### link标签
* **基本用法**
    ```html
    <link href="default.css" rel="stylesheet"title="Default Style">
    <link href="fancy.css" rel="alternate stylesheet" title="Fancy">
    <link href="basic.css" rel="alternate stylesheet" title="Basic">
    ```
    * 上面代码中，default.css是默认样式表，默认就会生效。fancy.css和basic.css是替换样式表（rel="alternate stylesheet"），默认不生效。
    * title属性在这里是必需的，用来在浏览器菜单里面列出这些样式表的名字，供用户选择，以替代默认样式表。**可以做主题**
* ``<link>``还可以加载网站的 favicon 图标文件。
    ```html
    <link rel="icon" href="/favicon.ico" type="image/x-icon">
    ```
* 手机访问时，网站通常需要提供不同分辨率的图标文件。
    ``` html 
    <link rel="apple-touch-icon-precomposed" sizes="114x114" href="favicon114.png">
    <link rel="apple-touch-icon-precomposed" sizes="72x72" href="favicon72.png">
    ```
* ``<link>``也用于提供文档的相关链接，比如下面是给出文档的 RSS Feed 地址。
    ```html
    <link rel="alternate" type="application/atom+xml" href="/blog/news/atom">
    ```
* **rel属性**
    * el属性表示外部资源与当前文档之间的关系，是<link>标签的必需属性。它可以但不限于取以下值。
    ```html
            <!-- 作者信息 -->
        <link rel="author" href="humans.txt"> author：文档作者的链接。
        <!-- 版权信息 -->
        <link rel="license" href="copyright.html">license：许可证链接。
        <!-- 另一个语言的版本 -->
        <link rel="alternate" href="https://es.example.com/" hreflang="es">alternate：文档的另一种表现形式的链接，比如打印版。
        <!-- 联系方式 -->
        <link rel="me" href="https://google.com/profiles/someone" type="text/html">
        <link rel="me" href="mailto:name@example.com">
        <link rel="me" href="sms:+15035550125">
        <!-- 历史资料 -->
        <link rel="archives" href="http://example.com/archives/">
        <!-- 目录 -->
        <link rel="index" href="http://example.com/article/">
        <!-- 导航 -->
        <link rel="first" href="http://example.com/article/">
        <link rel="last" href="http://example.com/article/?page=42">
        <link rel="prev" href="http://example.com/article/?page=1">prev：表示当前文档是系列文档的一篇，这里给出上一篇文档的链接
        <link rel="next" href="http://example.com/article/?page=3">next：系列文档下一篇的链接。
    ```

### 资源的预加载
* ``<link rel="preload">``告诉浏览器尽快下载并缓存资源（如脚本或样式表），该指令优先级较高，浏览器肯定会执行
    * rel="preload"除了优先级较高，还有两个优点：一是允许指定预加载资源的类型，二是允许onload事件的回调函数。下面是rel="preload"配合as属性，告诉浏览器预处理资源的类型，以便正确处理。
    * as属性指定加载资源的类型，它的值一般有下面几种。
    ```
    "script"
    "style"
    "image"
    "media"
    "document"
    ```
    * 如果不指定as属性，或者它的值是浏览器不认识的，那么浏览器会以较低的优先级下载这个资源。
    * 有时还需要type属性，进一步明确 MIME 类型
    ```html
    <link rel="preload" href="sintel-short.mp4" as="video" type="video/mp4">
    ```
    * 上面代码要求浏览器提前下载视频文件，并且说明这是 MP4 编码。
    * 所有预下载的资源，只是下载到浏览器的缓存，并没有执行。如果希望资源预下载后立刻执行，可以参考下面的写法。
* ``<link rel="prefetch">``的使用场合是，如果后续的页面需要某个资源，并且希望预加载该资源，以便加速页面渲染。该指令不是强制性的，优先级较低，浏览器不一定会执行。这意味着，浏览器可以不下载该资源，比如连接速度很慢时。
* ``<link rel="preconnect">``要求浏览器提前与某个域名建立 TCP 连接。当你知道，很快就会请求该域名时，这会很有帮助。
* ``<link rel="dns-prefetch">``要求浏览器提前执行某个域名的 DNS 解析
* ``<link rel="prerender">``要求浏览器加载某个网页，并且提前渲染它。用户点击指向该网页的链接时，就会立即呈现该页面。如果确定用户下一步会访问该页面，这会很有帮助。

* **media 属性**
    * media属性给出外部资源生效的媒介条件。
    ```html
    <link href="print.css" rel="stylesheet" media="print">
    <link href="mobile.css" rel="stylesheet" media="screen and (max-width: 600px)">
    ```
    * 上面代码中，打印时加载print.css，移动设备访问时（设备宽度小于600像素）加载mobile.css。
* 其他属性
    * ``<link>``标签的其他属性如下。
    * crossorigin：加载外部资源的跨域设置。
    * href：外部资源的网址。
    * referrerpolicy：加载时Referer头信息字段的处理方法。
    * as：rel="preload"或rel="prefetch"时，设置外部资源的类型。
    * type：外部资源的 MIME 类型，目前仅用于rel="preload"或rel="prefetch"的情况。
    * title：加载样式表时，用来标识样式表的名称。
    * sizes：用来声明图标文件的尺寸，比如加载苹果手机的图标文件
    
* ``<script>``
    * type属性给出脚本的类型，默认是 JavaScript 代码，所以可省略。完整的写法其实是下面这样。type属性也可以设成module，表示这是一个 ES6 模块，不是传统脚本
    * 对于那些不支持 ES6 模块的浏览器，可以设置nomodule属性。支持 ES6 模块的浏览器，会不加载指定的脚本。这个属性通常与type="module"配合使用，作为老式浏览器的回退方案。
    * ``<script>``还有下面一些其他属性，大部分跟 JavaScript 语言有关，可以参考相关的 JavaScript 教程。
        * async：该属性指定 JavaScript 代码为异步执行，不是造成阻塞效果，JavaScript 代码默认是同步执行。
        * defer：该属性指定 JavaScript 代码不是立即执行，而是页面解析完成后执行。
        * crossorigin：如果采用这个属性，就会采用跨域的方式加载外部脚本，即 HTTP 请求的头信息会加上origin字段。
        * integrity：给出外部脚本的哈希值，防止脚本被篡改。只有哈希值相符的外部脚本，才会执行。
        * nonce：一个密码随机数，由服务器在 HTTP 头信息里面给出，每次加载脚本都不一样。它相当于给出了内嵌脚本的白名单，只有在白名单内的脚本才能执行。
        * referrerpolicy：HTTP 请求的Referer字段的处理方法。
    
* ``<noscript>``标签用于浏览器不支持或关闭 JavaScript 时，所要显示的内容。用户关闭 JavaScript 可能是为了节省带宽，以延长手机电池寿命，或者为了防止追踪，保护隐私。
    ```html
    <noscript>
  您的浏览器不能执行 JavaScript 语言，页面无法正常显示。
    </noscript>
  ```
    上面这段代码，只有浏览器不能执行 JavaScript 代码时才会显示，否则就不会显示。

## 多媒体标签
### video标签
* ``<video>``标签是一个块级元素，用于放置视频。如果浏览器支持加载的视频格式，就会显示一个播放器，否则显示``<video>``内部的子元素。
```html
    <video src="example.mp4" controls>
    <p>你的浏览器不支持 HTML5 视频，请下载<a href="example.mp4">视频文件</a>。</p>
    </video>
```
* 上面代码中，如果浏览器不支持该种格式的视频，就会显示<video>内部的文字提示。

* `<video>`有以下属性。
    * src：视频文件的网址。
    * controls：播放器是否显示控制栏。该属性是布尔属性，不用赋值，只要写上属性名，就表示打开。如果不想使用浏览器默认的播放器，而想使用自定义播放器，就不要使用该属性。
    * width：视频播放器的宽度，单位像素。
    * height：视频播放器的高度，单位像素。
    * autoplay：视频是否自动播放，该属性为布尔属性。
    * loop：视频是否循环播放，该属性为布尔属性。
    * muted：是否默认静音，该属性为布尔属性。
    * poster：视频播放器的封面图片的 URL。
    * preload：视频播放之前，是否缓冲视频文件。这个属性仅适合没有设置autoplay的情况。它有三个值，分别是none（不缓冲）、metadata（仅仅缓冲视频文件的元数据）、auto（可以缓冲整个文件）。
    * playsinline：iPhone 的 Safari 浏览器播放视频时，会自动全屏，该属性可以禁止这种行为。该属性为布尔属性。
    * crossorigin：是否采用跨域的方式加载视频。它可以取两个值，分别是anonymous（跨域请求时，不发送用户凭证，主要是 Cookie），use-credentials（跨域时发送用户凭证）。
    * currentTime：指定当前播放位置（双精度浮点数，单位为秒）。如果尚未开始播放，则会从这个属性指定的位置开始播放。
    * duration：该属性只读，指示时间轴上的持续播放时间（总长度），值为双精度浮点数（单位为秒）。如果是流媒体，没有已知的结束时间，属性值为+Infinity。
        ```html
            <video width="400" height="400"
                autoplay loop muted
                poster="poster.png">
            </video>
        ```

* 上面代码中，视频播放器的大小是 400 x 400，会自动播放和循环播放，并且静音，还带有封面图。这是网站首页背景视频的常见写法。
  
* HTML标准没有规定浏览器需要支持哪些视频格式，完全是有浏览器厂商自己来决定。为了避免浏览器不支持视频格式，可以使用<source>标签，放置在同一个视频的多种格式。
    ```html
    <video controls>
        <source src="example.mp4" type="video/mp4">
        <source src="example.webm" type="video/webm">
        <p>你的浏览器不支持html5视频，请下载 <a href="example.mp4">视频文件</a>。</p>
        </video>
    ```
    * 注：这里<source>后面会讲，点击<a  href="#11" id="22">这里</a>转到
* 上面代码中，<source>标签的type属性的值是视频文件的 MIME 类型，上例指定了两种格式的视频文件：MP4 和 WebM。如果浏览器支持 MP4，就加载 MP4 格式的视频，不再往下执行了。如果不支持 MP4，就检查是否支持 WebM，如果还是不支持，则显示提示。

### audio标签（音频）
* `<audio>`标签是一个块级元素，用于放置音频，用法和<video>表标签基本一致。
    ```html
        <audio controls>
            <source src="foo.mp3" type="audio/mp3">
            <source src="foo.ogg" type="audio/ogg">
            <p>你的浏览器不支持 HTML5 音频，请直接下载<a href="foo.mp3">音频文件</a>。</p>
        </audio>
    ```
* 用法基本和视频播放标签<video>一致，大致属性差不多。
    常用<audio>属性：
        ```txt
            autoplay：      是否自动播放，布尔属性。
            controls：      是否显示播放工具栏，布尔属性。如果不设置，浏览器不显示播放界面，通常用于背景音乐。
            crossorigin：   是否使用跨域方式请求。
            loop：          是否循环播放，布尔属性。
            muted：         是否静音，布尔属性。
            preload：       音频文件的缓冲设置。
            src：           音频文件网址。
        ```
* ``<track>``视频播放字幕，在<video>标签中使用
    * 用法示例：
        ```html
                <video controls src="sample.mp4">
                    <track label="英文" kind="subtitles" src="subtitles_en.vtt" srclang="en">
                    <track label="中文" kind="subtitles" src="subtitles_cn.vtt" srclang="cn" default>
                </video>
        ```
        <track>主要属性:
            ```txt
                    label：    播放器显示的字幕名称，供用户选择。
                    kind：     字幕的类型，默认是subtitles，表示将原始声音成翻译外国文字，比如英文视频提供中文字幕。
                                    另一个常见的值是captions，表示原始声音的文字描述，通常是视频原始使用的语言，比如英文视频提供英文字幕。
                    src：      vtt 字幕文件的网址。
                    srclang：  字幕的语言，必须是有效的语言代码。
                    default：  是否默认打开，布尔属性。 
            ```
* `<source>`  <a id="11" href=“#22”>#</a>
    * 用于在<picture>、<video>、<audio>内指定一项外部的资源 单标签。
        * 主要属性为：
        ```txt
            type：     指定外部资源的 MIME 类型。
            src：      指定源文件，用于<video>和<audio>。
            srcset：   指定不同条件下加载的图像文件，用于<picture>。
            media：    指定媒体查询表达式，用于<picture>。
            sizes：    指定不同设备的显示大小，用于<picture>，必须跟srcset搭配使用。
        ```

* `<embed>`
    * 这个标签是嵌入一个外部内容，由浏览器控制，但不是所有都支持。
        * 嵌入视频播放器的例子：
            ```html
                <embed type="video/webm"
                    src="/media/examples/flower.mp4"
                    width="250"
                    height="200">
            ```
    * 主要通用属性
        * height：显示高度，单位为像素，不允许百分比。
        * width：显示宽度，单位为像素，不允许百分比。
        * src：嵌入的资源的 URL。
        * type：嵌入资源的 MIME 类型。
    * 下面是启动浏览器flash的例子
        ```html
            <embed src="whoosh.swf" quality="medium"
                bgcolor="#ffffff" width="550" height="400"
                name="whoosh" align="middle" allowScriptAccess="sameDomain"
                allowFullScreen="false" type="application/x-shockwave-flash"
                pluginspage="http://www.macromedia.com/go/getflashplayer">
                如果浏览器没有安装 Flash 插件，就会提示去pluginspage属性指定的网址下载。
        ```

* `<object>`,`<param>`
    * <object>是上面的<embed>的替代品，因为没有历史遗留的问题所以更推荐用，只限于插入少量几行代码
        * 下面是插入PDF文件的例子
        ```html
            <object type="application/pdf"
                data="/media/examples/In-CC0.pdf"
                width="250"
                height="200">
            </object>
        ```
        * 通用属性为：
            * data：嵌入的资源的 URL。
            * form：当前网页中相关联表单的id属性（如果有的话）。
            * height：资源的显示高度，单位为像素，不能使用百分比。
            * width：资源的显示宽度，单位为像素，不能使用百分比。
            * type：资源的 MIME 类型。
            * typemustmatch：布尔属性，表示data属性与type属性是否必须匹配。
    * `<param>` 能在里面来给<object>容器元素的标签使用来给出插件所要的运行参数。
        * ```html
                <object data="movie.swf" type="application/x-shockwave-flash">
                    <param name="foo" value="bar">
                </object>
            ```



## iframe（不常用）
### iframe
* `<iframe>` 主要用于在网页中来拼接其他的网页，不常用。
    * 示例：
        ```html
            <iframe src="https://www.example.com"
                width="100%" height="500" frameborder="0"
                allowfullscreen sandbox>
                <p><a href="https://www.example.com">点击打开嵌入页面</a></p>
            </iframe>
        ```
    * 主要属性
        ```txt
            allowfullscreen：允许嵌入的网页全屏显示，需要全屏 API 的支持，请参考相关的 JavaScript 教程。
            frameborder：   是否绘制边框，0为不绘制，1为绘制（默认值）。建议尽量少用这个属性，而是在 CSS 里面设置样式。
            src：           嵌入的网页的 URL。
            width：         显示区域的宽度。
            height：        显示区域的高度。
            sandbox：       设置嵌入的网页的权限，详见下文。
            importance：    浏览器下载嵌入的网页的优先级，可以设置三个值。high表示高优先级，low表示低优先级，auto表示由浏览器自行决定。
            name：          内嵌窗口的名称，可以用于<a>、<form>、<base>的target属性。
            referrerpolicy：请求嵌入网页时，HTTP 请求的Referer字段的设置。参见<a>标签的介绍。
        ```

* **sandbox**
    * 用于设置嵌入网页中的属性，相当于设置了一个隔离层
        ```html
            <iframe src="https://www.example.com" sandbox>
            </iframe>
        ```
    * 利用属性能设置具体的权限，主要的属性为：
        ```txt
            allow-forms：            允许提交表单。
        
            allow-modals：           允许提示框，即允许执行window.alert()等会产生弹出提示框的 JavaScript 方法。
        
            allow-popups：           允许嵌入的网页使用window.open()方法弹出窗口。
        
            allow-popups-to-escape-sandbox：允许弹出窗口不受沙箱的限制。
        
            allow-orientation-lock： 允许嵌入的网页用脚本锁定屏幕的方向，即横屏或竖屏。
        
            allow-pointer-lock：     允许嵌入的网页使用 Pointer Lock API，锁定鼠标的移动。
        
            allow-presentation：     允许嵌入的网页使用 Presentation API。
        
            allow-same-origin：      不打开该项限制，将使得所有加载的网页都视为跨域。
            
            allow-scripts：          允许嵌入的网页运行脚本（但不创建弹出窗口）。
        
            allow-storage-access-by-user-activation：  sandbox属性同时设置了这个值和allow-same-origin的情况下，允许<iframe>嵌入的第三方网页通过用户发起document.requestStorageAccess()请求，经由 Storage Access API 访问父窗口的 Cookie。
        
            allow-top-navigation：   允许嵌入的网页对顶级窗口进行导航。
        
            allow-top-navigation-by-user-activation：允许嵌入的网页对顶级窗口进行导航，但必须由用户激活。
        
            allow-downloads-without-user-activation：允许在没有用户激活的情况下，嵌入的网页启动下载。
        ```

### loading预加载
    * 设置资源的预加载有三个主要的属性
        * auto：浏览器默认行为
        * lazy： 懒加载网页即将滚动到在开始加载
        * eager：立即记载资源



## 表单标签
### from标签
* 标签用来定义一个表单，所有表单中的内容都要放在里面
* 示例：这是一个拥有用户名、文本输入框和提交按钮的表单
    
    ```html
        <form action="https://example.com/api" method="post">
            <label for="POST-name">用户名：</label>
            <input id="POST-name" type="text" name="user">
            <input type="submit" value="提交">
        </form>
    ```
    
* 主要属性为：
    ```html
        accept-charset   //服务器接受的字符编码列表，使用空格分隔，默认与网页编码相同。
        action           //指定接受并处理表单数据的服务器url地址
        autocomplete     //如果用户没有填写某个控件，浏览器是否可以自动填写该值。它的可能取值分别为off（不自动填写）和on（自动填写）。
        method           //提交数据的 HTTP 方法，可能的值有post（表单数据作为 HTTP 数据体发送），get（表单数据作为 URL 的查询字符串发送），dialog（表单位于<dialog>内部使用）。
        enctype          //当method属性等于post时，该属性指定提交给服务器的 MIME 类型。可能的值为application/x-www-form-urlencoded（默认值），multipart/form-data（文件上传的情况），text/plain。
        name             //表单的名称，应该在网页中是唯一的。注意，如果一个控件没有设置name属性，那么这个控件的值就不会作为键值对，向服务器发送。
        novalidate       //布尔属性，表单提交时是否取消验证。
        target           //在哪个窗口展示服务器返回的数据，可能的值有_self（当前窗口），_blank（新建窗口），_parent（父窗口），_top（顶层窗口），<iframe>标签的name属性（即表单返回结果展示在<iframe>窗口）。
    ```
* 常用的表单使用
    ``` 
    <form action="url地址" method="提交方式" name="表单名称">
        各种表单控件
    </form>
    ```

* **enctype**
    
    * 指定了使用post方法提交数据的时候，浏览器给出的mime类型
    * 属性有以下值：
        * 1、application/x-www-form-urlencoded是默认类型，控件名和控件值都要转义（空格转为*号，非数字和非字母转为%HH的形式，换行转为CR LF），控件名和控件值之间用=分隔。控件按照出现顺序排列，控件之间用&分隔
        * 2、multipart/form-data主要用于文件上传。这个类型上传大文件时，会将文件分成多块传送，每一块的 HTTP 头信息都有Content-Disposition属性，值为form-data，以及一个name属性，值为控件名。
        ```html
            <form action="https://example.com/api"
                enctype="multipart/form-data"
                method="post">
                用户名：<input type="text" name="submit-name"><br>
                文件：<input type="file" name="files"><br>
                <input type="submit" value="上传"> <input type="reset" value="清除">
            </form>
        ```

### fieldset和legend标签
* fieldset用于将一组相关控件组合到一起，是一个块级标签
* 有三个属性：
    * disabled：使控件不可用
    * form： 指定控件所属的from，值为id
    * name： 控件组的名称

### label标签

* 提供控件的文字说明，行内元素
### input标签

* 用来接收用户的输入，单标签
  
    * 默认值是text表示输入框
      
        开始
        
        * 属性的值
            ```html
                autofocus       //布尔属性，是否在页面加载时自动获得焦点。
                disabled        //布尔属性，是否禁用该控件。一旦设置，该控件将变灰，用户可以看到，但是无法操作。
                form            //关联表单的id属性。设置了该属性后，控件可以放置在页面的任何位置，否则只能放在<form>内部。
                list            //关联的<datalist>的id属性，设置该控件相关的数据列表，详见后文。
                name            //控件的名称，主要用于向服务器提交数据时，控件键值对的键名。注意，只有设置了name属性的控件，才会向服务器提交，不设置就不会提交。
                readonly        //布尔属性，是否为只读。
                required        //布尔属性，是否为必填。
                type            //控件类型，详见下文。
                value           //控件的值。
            ```
### 类型
* type决定了input的形式，以下为type值
#### 1、type=text 文本框
* 配套属性为
    ```html
        maxlength       //可以输入的最大字符数，值为一个非负整数。
        minlength       //可以输入的最小字符数，值为一个非负整数，且必须小于maxlength。
        pattern         //用户输入必须匹配的正则表达式，比如要求用户输入4个～8个英文字符，可以写成pattern="[a-z]{4,8}"。如果用户输入不符合要求，浏览器会弹出提示，不会提交表单。
        placeholder     //输入字段为空时，用于提示的示例值。只要用户没有任何字符，该提示就会出现，否则会消失。
        readonly        //布尔属性，表示该输入框是只读的，用户只能看，不能输入。
        size            //表示输入框的显示长度有多少个字符宽，它的值是一个正整数，默认等于20。超过这个数字的字符，必须移动光标才能看到。
        spellcheck      //是否对用户输入启用拼写检查，可能的值为true或false。
    ```
#### 2、type=search搜索框
* 用于搜索的文本框，基本和text相同
#### 3、type=button按钮
* 没有默认行为的按钮，可以指定click事件
    * 建议最好使用<button>标签代替，以来语义清晰，而来button标签里面可以插入图片和其他代码
#### 4、type=submit提交
* 提交按钮，点击按钮会把表单提交到服务器
* 指定value能切换显示的文字
    * 配套的主要属性
        ```html
            formaction      //提交表单数据的服务器 URL。
            formenctype     //表单数据的编码类型。
            formmethod      //提交表单使用的 HTTP 方法（get或post）。
            formnovalidate  //一个布尔值，表示数据提交给服务器之前，是否要忽略表单验证。
            formtarget      //收到服务器返回的数据后，在哪一个窗口显示。
        ```
####  5、type=image
* 表示将一个图像文件作为提交按钮，用法和submit一致,主要属性为
    ```html
            alt     //图像无法加载时显示的替代字符串。
            src     //加载的图像 URL。
            height  //图像的显示高度，单位为像素。
            width   //图像的显示宽度，单位为像素。
    ```
####  6、type=reset
* 是一个重置按钮，用户点击以后，所有表格控件重置为初始值。

* 7、`type=“checkbox”`
  
* 复选框，允许选择或取消选择该选项,checked属性表示默认选中,value属性的默认值是on
  
* 8、`type=“radio”`
* 单选框，表示一组选择之中，只能选中一项。单选框通常为一个小圆圈，选中时会被填充或突出显示
        * 1、checked：布尔属性，表示是否默认选中当前项。
        * 2、value：用户选中该项时，提交到服务器的值，默认为on'。

#### 9、type=email
* 只能输入电子邮箱的文本输入框。表单提交之前，浏览器会自动验证是否符合电子邮箱的格式，如果不符合就会显示提示，无法提交到服务器
    ```html
        maxlength       //可以输入的最大字符数。
        minlength       //可以输入的最少字符数。
        multiple        //布尔属性，是否允许输入多个以逗号分隔的电子邮箱。
        pattern         //输入必须匹配的正则表达式。
        placeholder     //输入为空时的显示文本。
        readonly        //布尔属性，该输入框是否只读。
    size            //一个非负整数，表示输入框的显示长度为多少个字符。
        spellcheck      //是否对输入内容启用拼写检查，可能的值为true或false。
    ```

#### 10、type=password
* 密码输入框，输入的字符会被遮挡
    ```html
        maxlength       //可以输入的最大字符数。
        minlength       //可以输入的最少字符数。
        pattern         //输入必须匹配的正则表达式。
        placeholder     //输入为空时的显示文本。
        readonly        //布尔属性，该输入框是否只读。
        size            //一个非负整数，表示输入框的显示长度为多少个字符。
    autocomplete    //是否允许自动填充，可能的值有on（允许自动填充）、off（不允许自动填充）、current-password（填入当前网站保存的密码）、new-password（自动生成一个随机密码）。
        inputmode       //允许用户输入的数据类型，可能的值有none（不使用系统输入法）、text（标准文本输入）、decimal（数字，包含小数）、numeric（数字0-9）等。
    ```

#### 11、type=file
* 文件选择框，允许用户选择一个或多个文件，常用于文件上传功能
    ```html
        accept      //允许选择的文件类型，使用逗号分隔，可以使用 MIME 类型（比如image/jpeg），也可以使用后缀名（比如.doc），还可以使用audio/*（任何音频文件）、video/*（任何视频文件）、image/*（任何图像文件）等表示法。
    capture     //用于捕获图像或视频数据的源，可能的值有user（面向用户的摄像头或麦克风），environment（外接的摄像头或麦克风）。
        multiple    //布尔属性，是否允许用户选择多个文件。
    ```

#### 12、type=hidden
* 不显示在页面的控件，用户无法输入它的值，主要用来向服务器传递一些隐藏信息。比如，CSRF 攻击会伪造表单数据，那么使用这个控件，可以为每个表单生成一个独一无二的隐藏编号，防止伪造表单提交
#### 13、type=number
* type=“number”是一个数字输入框，只能输入数字。浏览器通常会在输入框的最右侧，显示一个可以点击的上下箭头，点击向上箭头，数字会递增，点击向下箭头，数字会递减。
* 该类型有以下属性：
    ```html
        max             //允许输入的最大数值。
        min             //允许输入的最小数值。
    placeholder     //用户输入为空时，显示的示例值。
        readonly        //布尔属性，表示该控件是否为只读。
        step            //点击向上和向下箭头时，数值每次递减的步长值。如果用户输入的值，不符合步长值的设定，浏览器会自动四舍五入到最近似的值。默认的步长值是1，如果初始的value属性设为1.5，那么点击向上箭头得到2.5，点击向下箭头得到0.5。
    ```

#### 14、type=range
* 一个滑块，用户拖动滑块，选择给定范围之中的一个数值。因为拖动产生的值是不精确的，如果需要精确数值，不建议使用这个控件。常见的例子是调节音量,最大值max，最小值min，step步长值设置增长幅度。
* 和<datalist>标签配合使用，可以在滑动区域产生刻度
    ```html
        <input type="range" list="tickmarks">
            <datalist id="tickmarks">
            <option value="0" label="0%">
            <option value="10">
            <option value="20">
            <option value="30">
            <option value="40">
            <option value="50" label="50%">
            <option value="60">
            <option value="70">
            <option value="80">
            <option value="90">
            <option value="100" label="100%">
            </datalist>
    ```
#### 15、type=url
* 只能输入网址的文本框。提交表单之前，浏览器会自动检查网址格式是否正确，如果不正确，就会无法提交
```html
    <input type="url" name="url" id="url"
        placeholder="https://example.com"
        pattern="https://.*" size="30"
        required>
```
* 上面代码只能指定使用https协议
    * 该类型规定，不带有协议的网址是无效的，比如foo.com是无效的，http://foo.com是有效的。
* 配套属性为：  
    * maxlength：允许的最大字符数。
    * minlength：允许的最少字符串。
    * pattern：输入内容必须匹配的正则表达式。
* placeholder：输入为空时显示的示例文本。
    * readonly：布尔属性，表示该控件的内容是否只读。
    * size：一个非负整数，表示该输入框显示宽度为多少个字符。
    * spellcheck：是否启动拼写检查，可能的值为true（启用）和false（不启用）。

* 和<datalist>标签搭配使用，可以形成下拉列表供用户选择。随着用户不断键入，会缩小显示范围，只显示匹配的备选项，示例如下：
```html
    <input id="myURL" name="myURL" type="url" list="defaultURLs">
    <datalist id="defaultURLs">
    <option value="https://developer.mozilla.org/" label="MDN Web Docs">
    <option value="http://www.google.com/" label="Google">
    <option value="http://www.microsoft.com/" label="Microsoft">
<option value="https://www.mozilla.org/" label="Mozilla">
    <option value="http://w3.org/" label="W3C">
    </datalist>
```

#### 16、type=tel
* 只能输入电话号码的输入框。由于全世界的电话号码格式都不相同，因此浏览器没有默认的验证模式，大多数时候需要自定义验证

#### 17、type=date
* 只能输入日期的输入框，用户可以输入年月日，但是不能输入时分秒。输入格式是YYYY-MM-DD。

#### 18、type=time
* 只能输入时间的输入框，可以输入时分秒，不能输入年月日。日期格式是24小时制的hh:mm
* 如果包括秒数，格式则是hh:mm:ss。日期选择器的形式则随浏览器不同而不同

#### 19、type=color
* 一个选择颜色的控件，它的值一律都是#rrggbb格式。

#### 20、type=week
* 输入一年中第几周的输入框。格式为yyyy-Www，比如2018-W18表示2018年第18周。

#### 21、type=month
* 只能输入年份和月份的输入框，格式为YYYY-MM。

#### 22、type=datetime-local
    * 时间输入框，让用户输入年月日和时分，格式为yyyy-MM-ddThh:mm。注意，该控件不支持秒。

#### button按钮标签
* 没有默认行为的点击按钮，需要type属性和脚本指定的按钮功能
* <button>内部不仅放置文字，还可以放置图像，这可以形成图像按钮。
```html
    1、autofocus        //布尔属性，表示网页加载时，焦点就在这个按钮。网页里面只能有一个元素，具有这个属性。
    2、disabled         //布尔属性，表示按钮不可用，会导致按钮变灰，不可点击。
    3、name             //按钮的名称（与value属性配合使用），将以name=value的形式，随表单一起提交到服务器。
    4、value            //按钮的值（与name属性配合使用），将以name=value的形式，随表单一起提交到服务器。
    5、type             //按钮的类型，可能的值有三种：submit（点击后将数据提交给服务器），reset（将所有控件的值重置为初始值），button（没有默认行为，由脚本指定按钮的行为）。
    6、form             //指定按钮关联的<form>表单，值为<form>的id属性。如果省略该属性，默认关联按钮所在父表单。
    7、formaction       //数据提交到服务器的目标 URL，会覆盖<form>元素的action属性。
    8、formenctype      //数据提交到服务器的编码方式，会覆盖<form>元素的enctype属性。可能的值有三种：application/x-www-form-urlencoded（默认值），multipart/form-data（只用于文件上传），text/plain。
    9、formmethod       //数据提交到服务器使用的 HTTP 方法，会覆盖<form>元素的method属性，可能的值为post或get。
    10、formnovalidate  //布尔属性，数据提交到服务器时关闭本地验证，会覆盖<form>元素的novalidate属性。
    11、formtarget      //数据提交到服务器后，展示服务器返回数据的窗口，会覆盖<form>元素的target属性。可能的值有_self（当前窗口），_blank（新的空窗口）、_parent（父窗口）、_top（顶层窗口）。
```

#### select下拉标签
* 标签用于生成一个下拉菜单。
```html
    <label for="pet-select">宠物：</label>
    <select id="pet-select" name="pet-select">
    <option value="">--请选择一项--</option>
    <option value="dog">狗</option>
    <option value="cat">猫</option>
    <option value="others">其他</option>
    </select>
```
* 上面代码中，<select>生成一个下拉菜单，菜单标题是“--请选择一项--”，最右侧有一个下拉箭头。点击下拉箭头，会显示三个菜单项，供用户点击选择
* 属性如下：
```html
    1、autofocus        //布尔属性，页面加载时是否自动获得焦点。
    2、disabled         //布尔属性，是否禁用当前控件。
    3、form             //关联表单的id属性。
    4、multiple         //布尔属性，是否可以选择多个菜单项。默认情况下，只能选择一项。一旦设置，多数浏览器会显示一个滚动列表框。用户可能需要按住Shift或其他功能键，选中多项。
    5、name             //控件名。
    6、required         //布尔属性，是否为必填控件。
    7、size             //设置了multiple属性时，页面显示时一次可见的行数，其他行需要滚动查看。
```

#### option，optgroup标签
* <option>标签用在<select>、<optgroup>、<datalist>里面，表示一个菜单项，参见<select>的示例。
* option属性如下
```html
    1、disabled     //布尔属性，是否禁用该项。
    2、label        //该项的说明。如果省略，则等于该项的文本内容。
    3、selected     //布尔属性，是否为默认值。显然，一组菜单中，只能有一个菜单项设置该属性。
    4、value        //该项提交到服务器的值。如果省略，则等于该项的文本内容
```
* optgroup属性如下
```html
    1、disabled：布尔设置，是否禁用该组。一旦设置，该组所有的菜单项都不可选。
    2、label：菜单项的标题
```

* **<datalist>**
  
* 是一个容器标签，用于为指定控件提供一组相关数据，通常用于生成输入提示。它的内部使用<option>，生成每个菜单项。
  
* **<textarea>**
    * 一个块级元素，用来生成多行的文本框。
    * 标签属性如下
    ```html
        1、autofocus        //布尔属性，是否自动获得焦点。
        2、cols             //文本框的宽度，单位为字符，默认值为20。
        3、disabled         //布尔属性，是否禁用该控件。
        4、form             //关联表单的id属性。
        5、maxlength        //允许输入的最大字符数。如果未指定此值，用户可以输入无限数量的字符。
        6、minlength        //允许输入的最小字符数。
        7、name             //控件的名称。
        8、placeholder      //输入为空时显示的提示文本。
        9、readonly         //布尔属性，控件是否为只读。
        10、required        //布尔属性，控件是否为必填。
        11、rows            //文本框的高度，单位为行。
        12、spellcheck      //是否打开浏览器的拼写检查。可能的值有true（打开），default（由父元素或网页设置决定），false（关闭）。
        13、wrap            //输入的文本是否自动换行。可能的值有hard（浏览器自动插入换行符CR + LF，使得每行不超过控件的宽度），soft（输入内容超过宽度时自动换行，但不会加入新的换行符，并且浏览器保证所有换行符都是CR + LR，这是默认值），off（关闭自动换行，单行长度超过宽度时，会出现水平滚动条）。
    ```

* **<output>**
    * 标签是一个行内元素，用于显示用户操作的结果。
  
* **<progress>**
    * 标签是一个行内元素，表示任务的完成进度。浏览器通常会将显示为进度条。
    ```html
        <progress id="file" max="100" value="70"> 70% </progress>
    ```

* **<meter>**
    * 标签是一个行内元素，表示指示器，用来显示已知范围内的一个值，很适合用于任务的当前进度、磁盘已用空间、充电量等带有比例性质的场合。浏览器通常会将其显示为一个不会滚动的指示条。
    ```html
        1、min      //范围的下限，必须小于max属性。如果省略，则默认为0。
        2、max      //范围的上限，必须大于min属性。如果省略，则默认为1。
        3、value    //当前值，必须在min属性和max属性之间。如果省略，则默认为0。
        4、low      //表示“低端”的上限门槛值，必须大于min属性，小于high属性和max属性。如果省略，则等于min属性。
        5、high     //表示“高端”的下限门槛值，必须小于max属性，大于low属性和min属性。如果省略，则等于max属性。
        6、optimum  //指定最佳值，必须在min属性和max属性之间。它应该与low属性和high属性一起使用，表示最佳范围。如果optimum小于low属性，则表示“低端”是最佳范围；如果大于high属性，则表示“高端”是最佳范围；如果在low和high之间，则表示“中间地带”是最佳范围。如果省略，则等于min和max的中间值。
        7、form     //关联表单的id属性。
    ```

## 表格标签
### table,caption
* table是一个容器标签，所有的表格内容都要放置在里面
* caption是table里面的第一个内容，表示表格的标题
    ```html
        <table>
            <caption>示例表格</caption>
        </table>
    ```
### thead、tbody、tfoot     
* 这三个标签在table标签中表示表头、表体、表尾。使用不多
* 这三个元素都是可选的，在使用时thead总是最上面显示的，tbody其次，不管实际代码如何
* 可以同时在表给中来使用多个表体<tbody>

### colgroup、col
* colgroup和col都是空元素，colgroup用于包含一组列的定义，col来定义表格的一列属性
* 用colgroup来设置td或th属性就会直接给所有的单元格来赋值，而col可以通过span控制赋值表格数
* 另外col可以给表格申明结构，还能为表格引入样式；
    ```html
        <table>
            <colgroup>
                <col class="c1">
                <col class="c2">
                <col class="c3">
            </colgroup>
            <tr>
                <td>1</td>
                <td>2</td>
                <td>3</td>
            </tr>
        </table>
    ```

### tr

* tr表示表格的一行，<tr>放在<thead>、<tbody>、<tfoot>里面就会使用他们的排序
### td、th
* 这两个标签都是来定义表格的单元格的，th是标题单元格，td是内容数据单元格
* 其中需要注意的是
    * th 元素中的文本呈现为粗体并且居中。
    * td 元素中的文本是普通的左对齐文本。
        ```html
            <table>
                <tr>
                    <th>学号</th><th>姓名</th>
                </tr>
                <tr>
                    <td>001</td><td>张三</td> 
                </tr>
                <tr>
                    <td>002</td><td>李四</td>
                </tr>
            </table>
        ```
* `colspan`、`rowspan`属性
    * 主要用于跨行和跨列的情况
    * 前者表示跨越的栏数列数，后者表示跨越的行数，值为非负整数，默认为1，td属性
* `headers`属性
  
    * 这个属性是用来标识td属于哪个th的，通常在表格较大的时候使用，值绑定th的id值
* `scope`属性
    * 属性至支持th标签，决定th标签是栏的标题还是列的标题
    * 属性的值：
        ```txt
            row：该行的所有单元格，都与该标题单元格相关。
            col：该列的所有单元格，都与该标题单元格相关。
            rowgroup：多行组成的一个行组的所有单元格，都与该标题单元格相关，可以与rowspan属性配合使用。
            colgroup：多列组成的一个列组的所有单元格，都与该标题单元格相关，可以与colspan属性配合使用。
            auto：默认值，表示由浏览器自行决定。
        ```

## 语义化标签
* HTML5 添加了很多语义元素如下所示：
    * ``<article>``
        * 定义页面独立的内容区域。
    * ``<aside>``
        * 定义页面的侧边栏内容。
    * ``<bdi>``
        * 允许您设置一段文本，使其脱离其父元素的文本方向设置。
    * ``<command>``
        * 定义命令按钮，比如单选按钮、复选框或按钮
    * ``<details>``
        * 用于描述文档或文档某个部分的细节
    * ``<dialog>``
        * 定义对话框，比如提示框
    * ``<summary>``
        * 标签包含 details 元素的标题
    * ``<figure>``
        * 规定独立的流内容（图像、图表、照片、代码等等）。
    * ``<figcaption>``
        * 定义 ``<figure>`` 元素的标题
    * ``<footer>``
        * 定义 section 或 document 的页脚。
    * ``<header>``
        * 定义了文档的头部区域
    * ``<mark>``
     * 定义带有记号的文本。
    * ``<meter>``
        * 定义度量衡。仅用于已知最大和最小值的度量。
    * ``<nav>``
        * 定义导航链接的部分。
    * ``<progress>``
        * 定义任何类型的任务的进度。
    * ``<ruby>``
        * 定义 ruby 注释（中文注音或字符）。
    * ``<rt>``
        * 定义字符（中文注音或字符）的解释或发音。
    * ``<rp>``
        * 在 ruby 注释中使用，定义不支持 ruby 元素的浏览器所显示的内容。
    * ``<section>``
        * 定义文档中的节（section、区段）。
    * ``<time>``
     * 定义日期或时间。
    * ``<wbr>``
        * 规定在文本中的何处适合添加换行符.

## 自定义标签
```
myHero {
display: block;
background-color: #ddd;
padding: 50px;
font-size: 30px;
}
<myHero>我的第一个新元素</myHero>
```

## 浏览器低版本兼容
```
    <style>
    header, section, footer, aside, nav, main, article, figure {
        display: block; 
    }
</style>
第一种解决方案
<script>
    //创建nav自定义标签使页面内的nav标签起作用-然后display:block;
    document.createElement("nav");
</script>
第二种解决方案		引用js插件
最佳	在什么版本下执行该段代码	在低于ie 8或等于ie 8版本才会执行
<!--[if lte IE 8]>
<script type="text/javascript" src="HTML/语义标签兼容处理/html5shiv.min.js"></script>
<![endif]-->

<!--[if lt IE 9]
<script src="http://apps.bdimg.com/libs/html5shiv/3.7/html5shiv.min.js">
</script>
<![endif]-->

<!--[if lt IE 9]>
<script src="http://cdn.static.runoob.com/libs/html5shiv/3.7/html5shiv.min.js">
</script>
<![endif]-->
无语义标签
<div></div>
```


## 无语义标签
* ``<div></div>``
  
    * <div>是一个通用标签，表示一个区块（division）。它没有语义，如果网页需要一个块级元素容器，又没有其他合适的标签，就可以使用这个标签。
* ``<span></span>``
  
    * ``<span>``是一个通用目的的行内标签（即不会产生换行），不带有任何语义。它通常用作CSS样式的钩子，如果需要对某些行内内容指定样式，就可以把它们放置在
```html
带有语义的块级标签（比如<article>、<section>、<aside>、<nav>等）始终应该优先使用，当且仅当没有其他语义元素合适时，才可以使用<div>。
```



## 已经移除的元素
* 以下的 HTML 4.01 元素在HTML5中已经被删除:
    * ~~<acronym>~~
        * 标记一个首字母缩写
        * 用abbr代替
    * ~~<applet>~~
        * 一个嵌入式的java applet
        * 用object代替
    * ~~<basefont>~~
      * 规定页面上的默认字体颜色和字号
    * ~~<big>~~
        * ``<big>``标签呈现打字号字体效果。
        * 使用``<big>``标签可以很容易地放大字体。但是如果文字已是最大号字体，这时``<big>``标签将不起任何作用。
    * ~~<center>~~
       * 居中
       * 已用css样式代替
    * ~~<dir>~~
         * 定义目录列表
        * 用css来为列表添加样式
    * ~~<font>~~
        * 规定文本的字体，字体尺寸，字体颜色
        * 已用样式替代
    * ~~<frame>~~和~~<frameset>~~
        * ``<frame>``标签定义frameset中的一个特定的窗口（框架）
        * 示例：
        ```html
        <html>
             <frameset cols="25%,50%,25%">
                <frame src="frame_a.html">
                <frame src="frame_b.html">
                <frame src="frame_c.html">
             </frameset>
             </html>
        ```
    * ~~<noframes>~~
      
      * 为那些不支持框架的浏览器显示文本。
    * ~~<strike>~~
        * 定义加删除线文本定义
        * 用``<del>``代替
    * ~~<tt>~~
        * 定义打字机文本
        * 已用css代替