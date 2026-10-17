
iOS 图标将在 `ios/Runner/Assets.xcassets` 文件夹中创建/替换。桌面 macOS 系统应用图标可以在 `/macos/Runner/Assets.xcassets/Icon.appiconset/` 更新。Web 图标需要在 `web/icons/` 文件夹中更新。

# 发布 Android 应用

在本节中，你将获得关于构建和准备应用程序以发布到 Google Play Store（Play Store）的提示。如果这是你第一次在 Play Store 发布应用，你需要在发布平台上支付 25 美元的开发者注册费用进行注册（创建一个新的开发者账户）。

应用需要数字签名才能发布到 Google Play Store。Google Play Store 支持两种类型的产物：App Bundle 和 APK。

注意：在构建发布到 Play Store 之前，请确保运行了 `flutter analyze`。

## 创建密钥库 (Keystore)

你只需要为应用在商店中的生命周期创建一个密钥库。使用以下命令在相应环境中生成密钥库。`keystore.jks` 是密钥库文件，必须保持私密。

### 走向世界

```
keytool -genkey -v -keystore <path-to-dir>/keystore.jks
-keyalg RSA -keysize 2048 -validity 10000 -alias key
```

上述命令将询问你一些关于你组织的问题，你需要在命令行中提供这些信息。一旦你提供了所有必需信息，就会在指定目录生成 `keystore.jks`。如果你将此密钥库文件保留在项目目录中，请确保将其添加到 `.gitignore` 文件中，以避免意外提交到公共仓库。在此处了解更多关于创建密钥库的信息（创建密钥库）。

注意：`keytool` 随 Java 安装。运行 `flutter doctor -v` 来查找与 Android Studio 的 Java 二进制安装路径。

## 引用密钥库

在 `<flutter-project-root>/android` 文件夹中添加 `key.properties` 文件以引用 `keystore.jks` 和其他相关细节。同时在 `.gitignore` 中也添加 `key.properties` 文件。你不希望在版本控制中提交此文件。

```
storePassword=password created during keystore.jks generation
keyPassword=password created during keystore.jks generation
keyAlias=alias chosen during keystore.jks generation
storeFile=path-to-keystore/keystore.jks
```

## 签名配置

Android 应用的签名细节配置在 `<flutter-project-root>/android/app/build.gradle` 文件中。

### 加载 `key.properties`

配置细节从 gradle 文件中 `android {}` 块之前的 `key.properties` 加载。

```
def keystoreProperties = new Properties()
def keystorePropertiesFile = rootProject.file('key.properties')
if (keystorePropertiesFile.exists()) {
    keystoreProperties.load(new FileInputStream(keystorePropertiesFile))
}
```

### 318

### 实战型 Flutter

```
android {
}
//..
```

### 添加发布签名配置

```
...
android {
  signingConfigs {
    release {
      keyAlias keystoreProperties['keyAlias']
      keyPassword keystoreProperties['keyPassword']
      file(keystoreProperties['storeFile']) : null
      storePassword keystoreProperties['storePassword']
    }
  }
  buildTypes {
    release {
      signingConfig signingConfigs.release
    }
    debug {
      signingConfig signingConfigs.debug
    }
  }
}
```

注意：运行 `flutter clean` 命令以刷新 gradle 配置。

### 代码收缩

`minifyEnabled` 和 `shrinkResources` 设置为 `true` 可让 R8 代码缩减器（收缩、混淆和优化）自动移除运行时不需要的代码。

```
...
buildTypes {
  release {
    minifyEnabled true
    shrinkResources true
    signingConfig signingConfigs.release
  }
}
```

R8 代码缩减器在构建发布产物时默认启。。但是，可以通过在构建发布产物时传递 `--no-shrink` 标志来禁用它。

### 走向世界

## AndroidManifest.xml

AndroidManifest.xml 位于 `<flutter-project-root>/android/src/main/AndroidManifest.xml`。它用于定义应用的元数据、权限和组件。

## 构建配置

应用的配置定义在 `<flutter-project-root>/android/app/build.gradle` 的 `defaultConfig` 块中。

```
defaultConfig {
  applicationId "com.domain.app"
  minSdkVersion 18
  targetSdkVersion 28
  versionCode flutterCode.toInt()
  versionName flutterName
  multiDexEnabled true
}
```

### applicationId:

`applicationId` 包含应用的唯一 ID。一旦发布到 Play Store，它无法更改。

### minSdkVersion:

应用支持的最低 API 级别

### targetSdkVersion:

应用设计运行的目标。

### versionCode & versionName

这可以在 `pubspec.yaml` 的 `version` 属性中设置。versionCode 指定内部版本，而 versionName 指定显示字符串。`pubspec.yaml` 中的 `version` 指定为 `1.0.0+1`。第一部分 `1.0.0` 是 versionName，`+` 之后的所有是 versionCode。你可以在下方的 `pubspec.yaml` 中同时将 versionName 更新为 `1.0.1` 并将 versionCode 更新为 `2`：

```
version: 1.0.1+2
```

### 构建 APP bundle 是 是推荐的产物类型。在 Flutter 项目根目录下执行以下命令以构建 `.aab` 格式的发布产物。它生成在 `<flutter-project-root>/build/app/outputs/bundle/release/` 目录下。创建的产物是 `app-release.aab`。

```
flutter build appbundle
```

`app-release.aab` 包含了为 ARM32位 (armeabi-v7a)、64位 (arm64-v8a) 和 x86-64 编译的 Dart 和 Flutter 代码。每个目标应用接口 (ABI) 只有一个产物。

### 构建 APK

不支持 app bundle 格式的发布平台需要 APK 产物。默认情况下，一个 APK 包含所有平台/ABI 的原生二进制文件，这会导致用户向设备下载不适用的文件。在这种情况下，创建一个针对特定平台的 APK 是合理的。针对每个应用程序接口或 ABI 的 APK 产物可以使用以下命令创建：

```
flutter build apk --split-per-abi
```

上述命令将在多个 ABI 目标产物生成在 `<flutter-project-root>/build/app/outputs/flutter-apk/` 和 `<flutter-project-root>/build/app/outputs/apk/release` 目录下。两个目录中生成的产物均为：
