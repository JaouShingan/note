##  externals 使用外部插件

使用后，不会将该文件打包。

```javascript
    // 在webpack的配置文件中写入externals，并将要外部使用的插件放入externals对象内。
    externals: {
        jquery: 'jQuery'
    }
```
```html
    <!-- 在html内引入第三方插件的cdn -->
    <script src="https://cdn.bootcss.com/jquery/1.10.0/jquery.js"></script>
```

## DllPlugin

动态插件使用后，可以预先打包不会变化的插件，如echarts、react、vue、axios等，提高开发过程中的构建速度，提升开发效率。

插件分为两个部分，一个是预先打包的插件名为DllPlugin，一个是在正常构建中，引入已经打包好的插件的插件DllReferencePlugin