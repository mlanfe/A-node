### 常见的全局对象

1. console对象
   - console.trace()
   - console.clear()
2. process对象. 提供了node进程中相关的信息
   - process.argv 读取命令行执行传入的参数
   - process.env 可以存取环境变量
3. 特殊的全局对象
   - __dirname,  \_\_filename
   - exports, module, require()
   - 计时器的全局对象
     - setTimeout
     - setInterval
     - setImmediate
     - process.nextTick()
   -  **global对象 ** 使很多对象可以通过global来全局访问,  可以便于访问很多对象

### 模块化

#### 1. 没有模块化: 

1. 使用**iife**(immediately invoke function expression 立即执行函数)解决模块化问题 `(functiont bar() {})()`

#### 2. AMD模块化

#### 3. CommonJs模块化: 

##### 1.1 node是CommonJs在服务器端的一个实现 

- 每一个js文件都是一个单独的模块

- 每个模块中包括commonjs规范的核心变量**exports**, **module.exports**, **require**, 通过这些变量来进行**模块化开发**

  - 其实每个单独的js文件都是module的实例

  - module.exports == exports == requrie('./bar.js')

    ```javascript
    // bar.js文件中
    exports.name = 'Amy'
    exports.info = {
    	color: "red",
    	count: 20
    }
    
    //index.js文件中
    const bar = require('./bar')
    console.log(bar.name == 'Amy')  // true	
    ```

  - exports是通过module.exports来实现的。因为module.exports不是CommonJs的规范, 但是exports是CommonJs的规范, 所以nodejs为了实现这个规范, 在内部进行了赋值操作`exports=module.export`， 本质上导出的是`module.export`对象

    ```javascript
    // bar.js文件中
    exports.name = 'Amy'
    exports.info = {
    	color: "red",
    	count: 20
    }
    module.export = {
    	name: 'Jack'
    }
    
    //index.js文件中
    const bar = require('./bar')
    console.log(bar.name == 'Jack')  // true
    ```

##### 1.2 browserify是CommonJs在浏览器中的一种实现

#####  1.3 webpack打包工具具备对CommonJs的支持和转换





### 其他

1. 在终端执行node => global. => 按两次tab键可以查看global全局对象下的属性
