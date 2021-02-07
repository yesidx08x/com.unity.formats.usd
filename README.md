# com.unity.formats.usd
fix a bug.The plug-in has an infinite loop output, with new keyframe data superimposed on the original data each time.
防止软件锁死源码文件
>Unity\project\Package\manifest.json
文件修改"dependencies"部分，把"com.unity.formats.usd": "2.0.0-exp.1",

修改为
"com.unity.formats.usd": "file:../PackagesCustom/com.unity.formats.usd@2.0.0-exp.1", 

把整个插件包
D:\Unity\project\unity_test_usd\Library\PackageCache\com.unity.formats.usd@2.0.0-exp.1
全部复制到自建的
D:\Unity\project\unity_test_usd\PackagesCustom\com.unity.formats.usd@2.0.0-exp.1

unity自动刷新。
################################################

com.unity.formats.usd@2.0.0-exp.1
bug出现在UsdRecorderBehaviour.cs文件
由于插件无限循环输出，每次会有新的关键帧数据叠加到原来的数据上，在maya导入后动画曲线变成狗牙或锯齿。

解决方案，保证插件输出时的帧小于前一帧时，自动停止输出 。
UsdRecorderBehaviour.cs，修改ProcessRecording。
