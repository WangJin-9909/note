1、Winddows终端设置代理

set http_proxy=http://127.0.0.1:33210

set http_proxys=http://127.0.0.1:33210

2、局域网内里共享文件：

Step1. 进入到要共享的文件目录，打开terminal 

Step2. 调用 Python 一行代码启用静态文件服务器

如果安装的是Python2 执行：

​           python -m SimpleHTTPServer

如果安装的是Python3 执行：

​            python -m http.server    

**		python -m http.server 8000

另附：查看python版本

​           python -V

2、探索者：https://www.cryxr.xyz/

