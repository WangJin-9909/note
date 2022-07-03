小程序目录结构：

app.js          ：小程序初始化js

app.json     :   小程序配置文件，如:导航、窗口、各个页面引入

app.wxss: 小程序公共样式

Pages：各个子页面以js+json+wxml+wxss组成，方便管理，右边可快捷生成page;
小程序遵循MVC结构（Model View Controller）,js为页面逻辑（C&M）,wxss为页面样式，修饰wxml的DOM元素，wxml为页面机构（V），json为页面配置（具体API可见微信官方文档，可以修改此页面标题等，也充当了部分M）；







## app.json

pages：是一个数组，描述了页面，每一个页面占一个元素

window：系统配置，包括标题，标题颜色，标题背景等（如果不设置分页面配置则默认全覆盖）；

sitemapLocation：

tabBar：官方提供的导航功能，可以设置导航栏，list为导航数组，存放导航项、color为字体颜色、selectedcolor为选中颜色、