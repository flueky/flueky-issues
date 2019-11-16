## Flueky  的问题总结 

### AndroidStudio

1. AndroidStudio 在升级到**3.5**之后，格式化 xml 文件存在倒置 xml 元素位置。

通过修改 AndroidStudio 的配置属性。

<img src="pic/as/1.png"  width="600"/>
<img src="pic/as/2.png"  width="200"/>

2. 在  build.gradle 中使用  splits.density 打包出现错误。

    gradle 中还可以配置编译指定资源 resConfigs 。可能和 density 自定的资源发生冲突。配置只编译 xxhdpi 的目录，但是 density 中却配置编译 xhdpi 的目录。

3. 无法使用 google 仓库。

> Could not find method google() for arguments [] on repository container

主要是使用的 gradle 版本太低导致。需要升级到 4.x 以上。升级方式看各自的 AndroidStudio 配置。

<img src="pic/as/3.png"  width="600"/>

1. 使用默认目录，只需要修改  `gradle/wrapper/gradle-wrapper.properties` 路径下的版本。
2. 使用本机 gradle 目录，则需要升级 **Gradle home** 下的版本。


###  Android

1. xwalkview 截图黑屏

使用 `xwalkview.draw(canvas)` 方法截图黑屏 。

官方 API 示例。

```Java
xWalkView.captureBitmapAsync(new XWalkGetBitmapCallback() {

    @Override
    public void onFinishGetBitmap(Bitmap bitmap, int i) {
        imageView.setImageBitmap(bitmap);
    }
});
```

低版本可能没有上述。因此添加依赖。

```Gradle
maven {
            url 'https://download.01.org/crosswalk/releases/crosswalk/android/maven2'
        }
implementation 'org.xwalk:xwalk_core_library:23.53.589.4'
```

### git

1. git 新私有仓库并提交代码 not found 提示

新建私有仓库时，在本地 git 仓库中关联远程仓库后提交代码提示 not found ，需要在 .git/config 文件中，将用户名、密码添加到仓库地址前面。如
`https://username:password@github/user/repo.git`

### cmake

1. clion 中编译 c 工程出现下图错误。主要是升级 Xcode 导致升级对应的 sdk 。

<img src="pic/cmake/1.png"  width="900"/>

删除 CMakeCache.txt 文件，或整个 cmake 的 build 文件重新构建即可。