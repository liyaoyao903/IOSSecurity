# IOSSecurity
iOS安全，App加固保护原理
我们直接进图主题，就不说什么背景。

`我们可以从以下几个方面来保护我们的APP:`

### 字符串混淆
* 对应用程序中使用到的字符串进行加密，保证源码被逆向后不能看出字符串的直观含义。

### 类名、方法名混肴
* 对应用程序的方法名和方法体进行混淆，保证源码被逆向后很难明白它的真正功能。

### 程序结构混肴
* 对应用程序逻辑结构进行打乱混排，保证源码可读性降到最低。

### 反调试、反注入等一些主动保护策略
* 这是一些主动保护策略，增大破解者调试、分析APP的门槛。


#
#### 字符串加密 
* [字符串加密Demo](https://github.com/theKF/StringScurityDemo)<br>
字符串会暴露APP的很多关键信息，攻击者可以根据界面显示的字符串，快速找到相关逻辑的处理函数，从而进行分析破解。加密字符串可以增加攻击者阅读代码的难度以及根据字符串静态搜索的难度。<br><br>

比如一个APP中有如下的一些字符串定义在代码文件中：
![](https://github.com/theKF/IOSSecurity/blob/master/myfilexxx.png)<br>
经过加密后，代码文件变成如下的形式：<br>
![](https://github.com/theKF/IOSSecurity/blob/master/staicvoid.png)<br>
里面已经没有明文的字符串了，全是用byte的形式保存的，打包生成APP后，他们也就无法直观的看出实际内容了,这对破解者会造成巨大的难度：<br>
![](https://github.com/theKF/IOSSecurity/blob/master/tagscope.png)<br>

#
#### 符号混淆
* [方法名，变量名混淆Demo]()<br>
符号混淆的中心思想是将类名、方法名、变量名替换为无意义符号，提高应用安全性；防止敏感符号被class-dump工具提取，防止IDA Pro等工具反编译后分析业务代码。
<br>
比如一款混淆后的APP,用IDA等工具打开，如下图所示:
![](https://github.com/theKF/IOSSecurity/blob/master/entrypoint.png)<br>
“Labels”栏里，显示的这些符号，不管是类名还是方法名，谁也看不出来到底什么意思，这个函数到底是什么功能，就有点丈二和尚摸不着头脑的感觉，这就大大增加了破解者分析APP的难度。
