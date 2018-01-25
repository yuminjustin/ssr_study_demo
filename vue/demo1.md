vue最简单的服务端实现
 
 代码片段如下：


      'use strict';   //支持使用部分es6
       var express = require('express');   // express 做服务
       var router = express.Router();  // 路由
       var Vue = require("vue");
       var Renderer = require('vue-server-renderer').createRenderer();  // 服务端render
       var Com = require('../component/testvue') //引入vue自定义组件

       router.get('/', function (req, res, next) {
       
               Renderer.renderToString(Com, (err, html) => {
                      if (err) throw err
                      res.render("vue", { component: html });  //渲染到界面  模板 vue.html
                })
       });

       module.exports = router;   // 将此路由分支暴露
       
       
  自定义组件（testvue）：
  
           "use strict";
            var Vue = require('vue')

            module.exports = new Vue({
                template: `<div>Hello World Vue</div>`
            });
        
  模板（vue.html）：        
  
            <html>

                <head>
                    <title>vue Test</title>
                    <meta charset="utf-8" />
                </head>

                <body>
                        <div id="container">
                            <%-component%>
                        </div>
                         <!--使用ejs-->
                 </body>

             </html>
  
           
        
