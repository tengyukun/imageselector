# imageselector
图片选择器

 [原作者地址](https://github.com/lovetuzitong/MultiImageSelector/blob/master/README_zh.md)
 
 仿微信实现多图选择。支持单选和多选两种模式
 ![](https://github.com/lovetuzitong/MultiImageSelector/blob/master/art/select_1.png)
 ![](https://github.com/lovetuzitong/MultiImageSelector/blob/master/art/example_1.png)
 ![](https://github.com/lovetuzitong/MultiImageSelector/blob/master/art/select_2.png)
 ![](https://github.com/lovetuzitong/MultiImageSelector/blob/master/art/select_3.png)
 
### 运行DEMO

./gradlew installDebug
### 快速开始

* 第0步 把模块 multi-image-selector 作为你的项目依赖添加到工程中. 在项目build.gradle 中:
  
  repositories {
      maven { url "https://jitpack.io" }
  }

  dependencies {
      compile 'com.github.lovetuzitong:MultiImageSelector:1.2'
  }
  
* 第1步 在你的 AndroidManifest.xml 中做如下声明:

    <uses-permission android:name="android.permission.READ_EXTERNAL_STORAGE" />
    <uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />

    <application

      ...

      <!--Image Selector Entry-->
      <activity
          android:configChanges="orientation|screenSize"
          android:name="me.nereo.multi_image_selector.MultiImageSelectorActivity" />
    </application>
第2步 在你的代码中简单调用( 版本version-1.1之后支持 ), eg.
