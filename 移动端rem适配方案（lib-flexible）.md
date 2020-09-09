移动端rem适配方案（lib-flexible）

1.  准备工作(主要是 vue cli4中配置)

   - vue cli 创建好项目

     关于lib-flexible

       lib-flexible会自动在html的head中添加一个`meta name="viewport"`的标签，同时会自动设置html的font-size为屏幕宽度除以10，也就是1rem等于html根节点的font-size。假如设计稿的宽度是750px，此时1rem应该等于75px。假如量的某个元素的宽度是150px，那么在css里面定义这个元素的宽度就是 width: 2rem。但是当分辨率大于某个特定值时，它便不再生效。

2. 移动端适配步骤

   1.  一般而言，`lib-flexible`并不独立出现，而是搭配`px2rem-loader`一起做适配方案，目的是**自动将css中的px转换成rem**。以下为它在vue中的使用。 

      ````js
      npm install lib-flexible --save-dev
      npm install postcss-px2rem --save-dev
      ````

   2. #### 引入 lib-flexible

      -  在`main.js`中引入lib-flexible 

        ````js
        import 'lib-flexible'
        ````

   3. 接下来就是vue.config.js中配置

      ````js
      const px2rem = require("postcss-px2rem")
      
      module.exports = {
        css: {
            loaderOptions: {
                css: {},
                postcss: {
                    plugins: [ //插件
                        require('postcss-px2rem')({
                            // 以设计稿750为例， 750 / 10 = 75
                            remUnit: 37.5
                        }),
                    ]
                }
            }
        },
      };
      ````

   4. 基本已经完成，之后可以安装 fastclick ，解决移动端300ms延迟，图片懒加载等等

   5. 如果使用vscode开发 可以在cssrem这个插件修改字体大小，然后重启

      ![1599647281410](C:\Users\NB\AppData\Roaming\Typora\typora-user-images\1599647281410.png)

​           本文参考地址：https://www.jianshu.com/p/79be33f2ce88