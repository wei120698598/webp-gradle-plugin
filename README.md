# res-shrink-gradle-plugin [![](https://jitpack.io/v/wei120698598/img2webp.svg)](https://jitpack.io/#wei120698598/img2webp)

`res-shrink-gradle-plugin` has the following features for Android
1. Convert PNG/JPG/GIF to WEBP, shrink images;
2. Check duplicate resource;
3. Shrink resource filename and flatten folder hierarchy;
4. Hide resource filename extensions.

The plugin is work for aapt and aaptv2.
# Getting started

Step 1. Add it in your root build.gradle at the end of repositories:
```groovy
    buildscript {
        repositories {
            ...
            maven { url 'https://jitpack.io' }
    	}
    	dependencies {
            ...
            classpath "com.github.wei120698598:webp-gradle-plugin:Tag"
        }
    }
```
Step 2. Apply the plugin in your application build.gralde.
```groovy
    apply plugin: 'com.planb.res.shrink'
```

Share this release:
[![](https://jitpack.io/v/wei120698598/img2webp.svg)](https://jitpack.io/#wei120698598/img2webp)


# Config Webp Plugin
You can set some options for webp-gradle-plugin.

```groovy
ResShrinkOptions {
    //enable plugin, default true.
    def enabled = true
    
    //convert quality 0-100,suggest 50-100, default 75.
    def quality = 75
    
    //check image is duplicate, if both size equal, console will show error message , default true.
    def checkDuplicateEnabled = true
    
    //remove image by the regex, default null.
    def removeImgEnabled = true
   
    //enable resource proguard, enable
    def resProguardEnabled = true
   
    //print log, default true.
    def logEnabled = true
   
    //res-shrink-plugin-rules.pro file.
    File rulesFile
}
```
# Configure webp plugin enabled in different build types
Add it in your application build.gralde.
```groovy
afterEvaluate {
    tasks.each { task ->
        if (task.name.toLowerCase().contains("resShrink") && task.name.toLowerCase().contains("debug")) {
            task.enabled = false
        }
    }
}
```

# Configure `res-shrink-plugin-rules.pro`
Create `res-shrink-plugin-rules.pro` in your application directory.<br>
Support file path wildcard, each item is on a alone line or separated by `,` .<br>
The file path is by `res/` relative path or file name, such as`-dontshrink res/mipmap-hdpi/ic_launcher.png`or`-dontshrink ic_launcher.png` .<br>
<br>
Do not convert to webp images, use `-dontshrink`.<br>
Do not confuse resource files, use `-keep`.<br>
Resource files to delete, use `-assumenosideeffects`.<br>
Flatten package hierarchy, use `-flattenpackagehierarchy`.<br>
Increase security, hide file extensions, use `-optimizations`.<br>
# Plugin log
res-shrink-gradle-plugin will generate `{app}/build/outputs/webp/{buildType}/res-shrink-plugin-report.txt` file when built finish.
