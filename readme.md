
## 什么是 Html2Canvas
html2canvas 能够实现在用户浏览器端直接对整个或部分页面进行截屏。这个html2canvas脚本将当页面渲染成一个Canvas图片，通过读取DOM并将不同的样式应用到这些元素上实现。它不需要来自服务器任何渲染，整张图片都是在客户端浏览器创建。


## 关于兼容性
此插件只适用于APP项目（Android/Ios）、Web项目，不支持小程序！！

## 使用说明
1. 请先安装html2canvas，在项目根目录执行 npm install html2canvas --save
2. 为避免出现跨域问题，建议将图片转为Base64字符串后使用。
3. 该插件最终输出的图片文件为Base64格式，需搭配[image-tools](https://ext.dcloud.net.cn/plugin?id=123)将图片保存到临时目录，再次感谢该插件作者！
4. 确保在dom完成渲染后，再传入DomId，受限于[renderjs](https://uniapp.dcloud.io/frame?id=renderjs)的通信机制，目前只能通过这个方式来通知html2canvas执行操作。
5. 本插件仅基于renderjs做封装演示，[html2canvas官网](http://html2canvas.hertzen.com/documentation)有更多参数可根据业务场景自由定制。

## 传入参数
|  属性名  |  是否必填  |  值类型  |  说明  |
|  ----  | ----  |  ----  |  ----  |
| domId  | 是 | String | Dom节点id名称，保证在渲染完毕后再赋值 |



## 事件
|  属性名  |  是否必填  |  值类型  |  说明  |
|  ----  | ----  |  ----  |  ----  |
| @renderFinish  | 是 | String | html2canvas执行完毕后通知组件，Base64参数 |

