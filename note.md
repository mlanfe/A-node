node.js是一个基于v8引擎的js运行时环境(chrome也嵌入了v8引擎)



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

#### 2. AMD模块化, CMD模块化

#### 3. CommonJs模块化: 

##### 3.1 node是CommonJs在服务器端的一个实现 

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
    
    
    
  - [require()的查找规则](https://nodejs.org/docs/latest/api/modules.html#all-together)
  
  - 
  
    ```javascript
    
    ```

##### 3.2 browserify是CommonJs在浏览器中的一种实现

#####  3.3 webpack打包工具具备对CommonJs的支持和转换

#### 4. ES Module. (ES自己的模块化系统)

 1. import和export是关键字, 不是函数. **编译时解析/静态解析**

    [import和export的语法细节](https://es6.ruanyifeng.com/#docs/module#%E6%A6%82%E8%BF%B0)

 2. 存在import()函数, 动态引入

 3. js引擎遇到import时会**异步加载**js文件, 不会阻塞主线程继续执行

    ```html
    // 其中foo中的代码将在bar中的代码前面执行
    <script src='./bar.js' type='module'></script>
    <script src='./foo.js'></script>
    
    ```

 4. wes



#### 5. commonjs模块和es module对比

1. 多次引入, 只加载运行一次
2. 如果存在循环引入, 那么加载时是深度优先算法

3. 模块的导入和导出

   1. es6的模块:
      - 在导入文件中: 相当于导入用const定义的变量: 不可以改变基本类型值, 可以改变引用类型值的某个属性
      -  在被导入文件中: 改变基本类型值和引用类型值会影响其他文件导入的这个变量
      - 为了避免难以纠错, 应该尽量避免在导入文件中改变被导入文件中的变量的属性

   2. commonjs模块中:

      -  在导入文件中: 导入是对module.exports对象的浅拷贝对象; 改变基本类型值不影响被导入文件中的变量, 改变引用类型值会影响被导入文件中的变量

      - 在被导入文件中: 改变基本类型值不会影响其他文件导入的这个变量; 改变引用类型值会影响其他文件导入的这个变量

   3. CommonJS 模块输出的是一个值的拷贝，ES6 模块输出的是值的引用。
   4. CommonJS 模块是运行时加载，ES6 模块是编译时输出接口。
   5. CommonJS 模块的require()是同步加载模块，ES6 模块的import命令是异步加载，有一个独立的模块依赖的解析阶段。





### 其他

1. 在终端执行node => global. => 按两次tab键可以查看global全局对象下的属性
