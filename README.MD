## 介绍
这是一个简化上传到jcenter的简单脚本

## 使用方法

#### 编辑gradle.properties 文件
gradle.properties 文件有两个地方，一个在项目本身里，一个在系统里。我建议这种每次都一样的配置直接放在系统里面

```bash
#在Mac上，打开终端输入（把用户名替换成自己的）
vi /Users/用户名/.gradle/gradle.properties 
```
加入

```
#jcenter 上的用户名和api key
BINTRAY_USER=userName
BINTRAY_KEY=apikey

#开发者信息
DEVELOPER_ID=HANGOX
DEVELOPER_NAME=hangox
DEVELOPER_EMAIL=liang.hanguang93@gmail.com

```
退出保存即可。

#### 编辑项目的build.gradle
加入两个插件的引用

```gradle
buildscript {
    repositories {
        jcenter()
    }
    dependencies {
        classpath 'com.android.tools.build:gradle:2.2.0'
        classpath 'com.jfrog.bintray.gradle:gradle-bintray-plugin:1.7'
        classpath 'com.github.dcendents:android-maven-gradle-plugin:1.5'

        // NOTE: Do not place your application dependencies here; they belong
        // in the individual module build.gradle files
    }
}
```

#### 编辑library 的build.gradle

在想要上传的module的build.gradle加入

```groovy
ext{
    eGroup = 'com.hangox'
    eArtifactId = 'polygon-imageview'
    eName = "polygonImageView"
    eDescription = ''
    eVersion = '1.0'
    eVcsUrl = 'https://github.com/hangox/PolygonImageView.git'
    eVcsTag = 'v1.0' //git tag的名字,可以为空
    eWebsiteUrl = 'https://github.com/hangox/PolygonImageView'

}

//这一行不用的时候建议注释掉，因为国外DNS的原因，有时候会找不到dns的,导致编译失败
apply from : "https://raw.githubusercontent.com/hangox/bintray-push/v1.0/upload.gradle"
```

最后的项目引用将会是这样：`eGroup:eArtifactId:eVersion`
对于我这个项目，也就是 `com.hangox:polygon-imageview:1.0`


#### 开始上传

运行

```gradle
gradle bintrayUpload
```

#### jcenter 上申请通过

## 感谢

[gradle-publish](https://github.com/msdx/gradle-publish)



