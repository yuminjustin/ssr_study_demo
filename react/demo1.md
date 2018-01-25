 react最简单的服务端实现
 
 代码片段如下：


      'use strict';   //支持使用部分es6
       var express = require('express');   // express 做服务
       var router = express.Router();  // 路由
       require("node-jsx").install();  //安装"node-jsx"，安装该模块可以使nodejs兼容jsx语法
       var React = require("react");
       var ReactDOMServer = require("react-dom/server");  //服务端reactdom
       
       var Com = require('../component/test').Component //引入自定义react组件

       router.get('/', function (req, res, next) {
       
               var html = ReactDOMServer.renderToString(Com({ name: "Hello World React" }))   
               //向组件传参，并使用renderToString方法解析成html字符串
               
               res.render("react", { component: html });  //渲染到界面   模板是react.html
       });

       module.exports = router;   // 将此路由分支暴露
       
       
  自定义组件（test）：
  
         "use strict";
          var React = require("react");
          var Component = React.Component;

          class Test extends Component {
                render() {
                      return <h1>{this.props.name}</h1>;
                }
          }
          
          module.exports = {
                "Component": function (props) {
                      // {...props}   三点运算符 会报错  并不能完全支持es6 可能需要安装babel 支持
                     return <Test name={props.name} />
                  }
           };
        
  模板（react.html）：        
  
            <html>

                <head>
                    <title>react Test</title>
                    <meta charset="utf-8" />
                </head>

                <body>
                        <div id="container">
                            <%-component%>
                        </div>
                         <!--使用ejs-->
                 </body>

             </html>
  
           
        
