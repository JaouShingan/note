# uni-app 学习

## [pages.json](https://uniapp.dcloud.io/collocation/pages)

1、[pages](https://uniapp.dcloud.io/collocation/pages?id=pages)

    数组，存放页面，数组内第一项表示启动页，每一项的内部style可以覆盖全局样式

2、[globalStyle](https://uniapp.dcloud.io/collocation/pages?id=globalstyle)

    全局样式设置

3、[tabBar](https://uniapp.dcloud.io/collocation/pages?id=tabbar)

    底部导航条，list参数里至少两个选项。

4、[condition](https://uniapp.dcloud.io/collocation/pages?id=condition) 
    
    仅在开发时有效，用于模拟直达页面的场景

## [系统基本组件](https://uniapp.dcloud.io/component/README)

1、[text](https://uniapp.dcloud.io/component/text)

    文本组件。类似于span

2、[view](https://uniapp.dcloud.io/component/view)

    视图容器。类似于div

    hover-stop-propagation 禁止hover冒泡到父级

3、[button](https://uniapp.dcloud.io/component/button)

    按钮

4、[image](https://uniapp.dcloud.io/component/image)

    图片。组件默认宽度 300px、高度 225px；

    属性mode，设置图片显示类型。默认为scaleToFill不保持纵横比缩放图片，使图片的宽高完全拉伸至填满 image 元素。

## 样式

-   rpx 响应式px

-   @import 导入外联样式表，如

        @import url("./a.css");

-   支持基本常用选择器，如id、class、element选择器

-   uniapp中不能使用 * 选择器

-   page相当于body节点

-   定义在App.vue中的样式为全局样式，作用于每一个页面。在pages目录下的vue文件中定义的样式为局部样式，只作用在对应的页面，并会覆盖App.vue中相同的选择器

-   uniapp支持使用字体图标，注意：

    -   字体文件小于40kb，uniapp会自动转为base64格式
    -   大于40kb，需要开发者自己转换，否则不生效
    -   字体文件的引用路径推荐使用以~@开头的绝对路径
    ```css
        @font-face {
            font-family: test1-icon;
            src: url('~@/static/iconfont.ttf');
        }
    ```
    使用：1、将font字体库放入static文件夹下，（主要包含.css、.eot、.svg、.ttf、.woff、.woff2六个文件）。
    2、将iconfont.css文件里的文件引用路径（非base64）加~@/static/[目录]
    3、在全局App.vue里的style里引入iconfont.css文件
    ```css
        @import url("./static/fonts/iconfont.css");
    ```
    4、在项目里使用
    ```html
        <view class="iconfont icon-tupian"></view>
    ```

-   scss\less的使用

    在hbuilderx里安装插件

## 数据绑定

    同vue一样。在data里定义数据即可。

-   数据绑定

    v-bind:src="url" 或 :src="url"

-   事件绑定

    v-on:click="clickFoo" 或 @click="clickFoo"

    传参: @click="clickFoo(arg1, arg2, $event)"

    $event是点击事件，可放在参数任意位置

## 生命周期

-   [uni-app的生命周期](https://uniapp.dcloud.io/collocation/frame/lifecycle)

-   [页面的生命周期](https://uniapp.dcloud.io/collocation/frame/lifecycle?id=%e9%a1%b5%e9%9d%a2%e7%94%9f%e5%91%bd%e5%91%a8%e6%9c%9f)

-   [组件的生命周期](https://uniapp.dcloud.io/collocation/frame/lifecycle?id=%e7%bb%84%e4%bb%b6%e7%94%9f%e5%91%bd%e5%91%a8%e6%9c%9f)

## 下拉刷新

-   开启下拉刷新

    -   可以全局配置

        在pages.json文件的globalStyle对象里配置enablePullDownRefresh为true，即可全局开启下拉刷新。

    -   页面配置

        在pages.json文件的pages对象里的对应页面内的style对象里没值enablePullDownRefresh为true，即可让对应页面开启下拉刷新

    -   页面内通过代码开启下拉刷新

        uni.startPullDownRefresh()

-   监听下拉刷新

    在页面内可以通过同onShow平级的onPullDownRefresh方法，进行监听。当触发下拉刷新后，系统将会执行onPullDownRefresh方法。当onPullDownRefresh方法内的代码执行完毕之后，应当使用uni.stopPullDownRefresh();停止刷新状态的显示。

## 上拉刷新

    onReachBottom 方法可以监听触底。

    onReachBottomDistance属性可以设置触底时距离底部的距离。可以全局配置，也可以在某一个页面配置

## [发起请求](https://uniapp.dcloud.io/api/request/request)

    使用uni.request(OBJECT)发起请求

## [数据缓存](https://uniapp.dcloud.io/api/storage/storage)


## [上传图片、预览图片](https://uniapp.dcloud.io/api/media/image)

-   上传图片uni.chooseImage

-   预览图片uni.previewImage

## [跨端兼容](https://uniapp.dcloud.io/platform)

-   html中
    ```html
    <!-- #ifdef [平台代码] -->
        <view></view>
    <!-- #endif -->
    ```
-   js中
    ```js
    // #ifdef [平台代码]
        console.log('平台')
    // #endif
    ```
-   css中
    ```css
    /* #ifdef [平台代码] */
	color: pink;
	/* #endif */
    ```

## 导航跳转、传参

-   声明式导航跳转

    [navigator](https://uniapp.dcloud.io/component/navigator) 组件

    -   open-type: 跳转方式，根据不同设置可以有不同的跳转结果。
        -   switchTab   允许跳转至tabBar里的页面
        -   redirect    先将上一个页面卸载，跳转后不能反回上一个页面

-   [编程式导航跳转](https://uniapp.dcloud.io/api/router)


-   传参
    直接在路由地址后面以query的方式添加即可

-   接收
    在目标组件的onLoad方法参数即是路由传递的参数

## 创建组件

## 组件通信

-   父传子

-   子传父

-   兄弟组件