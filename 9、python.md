直接输入`pip install 你想要安装的第三方库`（这里我还是以numpy为例）

![1655793413959](C:\02.code\note\img\1655793413959.png)





（1）pip 自身的升级

py -m pip install --upgrade pip

（2）pip安装/卸载/升级

pip install 包名              #安装
pip uninstall 包名            #卸载
pip install --upgrade 包名    #升级

（3）pip查看已安装的包

pip list

（4）pip检查哪些包需要更新：

pip list --outdated

（5）pip查看某个包的详细信息：

pip show 包名

（6）pip安装指定版本的包：pip install 包名==版本号
例如：
pip install numpy==1.20.3
pip install 'matplotlib>3.4'
pip install 'matplotlib>3.4.0,<3.4.3'  #可通过使用==, >=, <=, >, <来指定版本
