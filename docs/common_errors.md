# 常见错误

## 如果调试时遇到transform函数处理 call指令时函数找不到的问题

这是unity代码裁剪引起的。你需要在主工程中显式带上类或者函数的使用，如RefTypes.cs所做的那样。

如果你是新使用huatuo的项目。建议将 [huatuo_trail](https://github.com/focus-creative-games/huatuo_trial)/Assets/Main/HuatuoLib 拷贝到你主工程，
然后再在RefTypes.cs里添加你要引用的类型。

## 凡是遇到FileLoadException：xxxxxx/StreamingAssets/HotFix.dll 错误的问题

这是il2cppd代码里面抛出的，原因是在编译之前没有替换huatuo源码中的libil2cpp目录

解决办法：

  1. 确定已经将了huatuo代码中的 libil2cpp 目录替换了对应的Editor 中的 libil2cpp 目录
  2. 删除Unity工程中的Library目录，重新构建即可

## Assembly.Load(byte[]) 出错: NotSupportedException

原因是你的huatuo太旧，未实现Load(byte[])这个函数。 拉最新的huatuo，替换你的libil2cpp，重新打包就行了

## 更新huatuo代码（替换libil2cpp）后发现更新未生效
这是由于之前使用过旧代码编译导致的，Library 是旧的。只要删掉Library在重新打包就可以了

## 打包生成Visual Studio Project后，编译出现错误找不到Windows SDK版本或无法打开.....\binUnityPlayerStub.lib
  打包生成的C++工程中，依赖关系为：项目主工程（同unity项目名，当前启动项目）依赖Il2CppOutputProject，Il2CppOutputProject依赖UnityPlayerStub。但是生成的工程设置中并没有设置依赖，一般按照下面的设置就能解决：
  1. 编译UnityPlayerStub项目，遇到问题就修改项目设置里面的 Windows SDK Version 和 Platform Toolset
  2. 编译Il2CppOutputProject 项目
  3. 启动成功
