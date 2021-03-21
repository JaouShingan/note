# webpack笔记

## 配置项

### externals 使用外部插件

使用后，不会将该文件打包。

```javascript
// 在webpack的配置文件中写入externals，并将要外部使用的插件放入externals对象内。
externals: {
    jquery: 'jQuery';
}
```

```html
<!-- 在html内引入第三方插件的cdn -->
<script src="https://cdn.bootcss.com/jquery/1.10.0/jquery.js"></script>
```

## loader/加载器

1、url-loader

有三个默认选项：limit、fallback、mimetype

limit

Type: Number|Boolean|String Default: undefined
当在设定值范围内时，将匹配的文件转换为 Data URL 。当超过时，将文件传给fallback设定的loader处理。

fallback

Type: String Default: 'file-loader'
当匹配文件超过设定值后，将会进入fallback所指定的loader进行处理。并且url-loader的options将会传给fallback所指定的loader。

mimetype

Type: String Default: (file extension)


## Plugin/插件

### DllPlugin

动态插件使用后，可以预先打包不会变化的插件，如 echarts、react、vue、axios 等，提高开发过程中的构建速度，提升开发效率。

插件分为两个部分，一个是预先打包的插件名为 DllPlugin，一个是在正常构建中，引入已经打包好的插件的插件 DllReferencePlugin。

-   配合 vue-cli 3 使用

    在项目根目录下新建文件 webpack.dll.config.js

    ```javascript
    const DllPlugin = require('webpack/lib/DllPlugin');

    const path = require('path');
    // 清理打包输出时的文件夹 /dist
    const { CleanWebpackPlugin } = require('clean-webpack-plugin');

    module.exports = {
        mode: 'production',
        entry: {
            vendor: ['core-js', 'vue', 'axios', 'vue-router']
        },
        output: {
            // 输出文件名
            filename: '[name].dll.js',
            // 输出文件存放地址
            path: path.resolve(__dirname, './dll'),
            // 全局库名
            library: 'dll_[name]'
        },
        plugins: [
            new CleanWebpackPlugin(),
            new DllPlugin({
                /*
                    该插件的 name 属性值需要和 output.library 保存一致，该字段值，也就是输出的 manifest.json 文件中 name 字段的值。
                    比如在 jquery.manifest 文件中有 name: '\_dll_jquery'
                    */
                name: 'dll_[name]',
                /* 生成 manifest 文件输出的位置和文件名称 */
                path: path.join(__dirname, './dll', '[name].manifest.json')
            })
        ]
    };
    ```

    在根目录下启用 vue.config.js 文件

    ```javascript
        // 添加如下配置
        configureWebpack: {
            plugins: [
                new DllReferencePlugin({
                    context: __dirname,
                    manifest: require('./dll/vendor.manifest.json')
                }),
    	    ],
        }
    ```

    在 package.json 文件中添加命令

    ```json
        "scripts": {
            "dll": "webpack --config webpack.dll.config.js"
        }
    ```

    在 public/index.html 文件中添加如下代码，用于将 dll 命令预先打包好的文件引入开发环境项目中

    ```html
    <script src="./dll/vendor.dll.js"></script>
    ```

    完成后，须先执行一次命令

        npm run dll

    然后执行启动项目的命令即可

    > 注意要点：
        1、dll命令打包生成的文件最好单独放一个文件目录下，如文中写到的dll。
        2、在配置vue.config.js文件时，一定要确保context的值要正确。否则还是会将所有的文件一起打包。
