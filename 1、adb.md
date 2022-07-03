1、使用adb打开浏览器，并打开百度

adb shell  am start -a android.intent.action.VIEW -d http://www.baidu.com

2、查看性能指令

adb shell dumpsys gfxinfo 【包名】

3、输入文本

adb shell input text  文本

