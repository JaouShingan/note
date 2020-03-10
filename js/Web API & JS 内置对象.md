# Web API

## [Blob](https://developer.mozilla.org/zh-CN/docs/Web/API/Blob)

### 构造函数

    Blob(blobParts[, options])

### 方法

    Blob.arrayBuffer()

        返回一个promise且包含blob所有内容的二进制格式的 ArrayBuffer

## [File](https://developer.mozilla.org/zh-CN/docs/Web/API/File)

继承自Blob

### 构造函数

    File()

        返回一个新构建的文件对象（File）。



# JS 内置对象

## [ArrayBuffer](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/ArrayBuffer)

不能直接操作 ArrayBuffer 的内容，而是要通过**类型数组对象**或 **DataView 对象**来操作

### 语法

    new ArrayBuffer(length)

## [DataView](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/DataView)

视图是一个可以从 二进制ArrayBuffer 对象中读写多种数值类型的底层接口，使用它时，不用考虑不同平台的字节序问题。

### 语法

    new DataView(buffer [, byteOffset [, byteLength]])

### 方法

    DataView.prototype.getUint8()

        从DataView起始位置以byte为计数的指定偏移量(byteOffset)处获取一个8-bit数(无符号字节).

    DataView.prototype.setUint8()

        从DataView起始位置以byte为计数的指定偏移量(byteOffset)处储存一个8-bit数(无符号字节).