# Demo-gradle
通常情况下 使用AS创建项目，会默认配置好gradle信息，gradle还能够发挥哪些作用，在此扩展尝试下
## gradle统一配置 编译sdk,tool等版本信息
```
//-------gradle 统一依赖管理
/*在根目录中配置公用供子模块调用*/
ext {
    //Android
    compileSdkVersion = 26
    buildToolsVersion = "26.0.2"
    minSdkVersion = 15
    targetSdkVersion = 26

    //Version
    supportLibrary = "26.+"

    //supportLibraries dependencies
    supportDependencies = [
            supportAppcompat: "com.android.support:appcompat-v7:${supportLibrary}",
    ]
}
```
## gradle实现多渠道打包
```
 //---多渠道打包 1/3
    //签名配置
    signingConfigs {
        debug {
            // 指定 debug证书
            //todo 如果配置了release 无法打出 debug包, 还不知道原因
            storeFile file("${rootDir}/keystores/debug.keystore")
        }

        release {
            storeFile file("${rootDir}/keystores/test.jks") //release证书
            storePassword "testtest"                         //签名证书密码
            keyAlias "test"                                 //别名
            keyPassword "testtest"                           //别名密码
        }
}
```



