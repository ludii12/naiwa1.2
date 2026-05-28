# 奶娃 APP 构建说明

## 项目位置
所有项目文件位于 `/workspace/naiwa-app/`

## 在本地电脑构建APK的步骤

### 1. 安装必要的工具

确保你的电脑已安装：
- **Node.js** (v16 或更高版本)
- **Java JDK** (v17 或更高版本)
- **Android Studio** 或 Android SDK

### 2. 复制项目到本地

```bash
# 将整个 naiwa-app 文件夹复制到你的电脑
scp -r user@server:/workspace/naiwa-app ./
```

或者直接在本地创建新项目（如果上述方法不可用）。

### 3. 安装依赖

```bash
cd naiwa-app
npm install
```

### 4. 构建Web应用

```bash
npm run build
```

### 5. 同步到Android项目

```bash
npx cap sync android
```

### 6. 使用Android Studio构建APK

打开 Android Studio，选择 "Open an existing project"，然后打开 `naiwa-app/android` 文件夹。

或者使用命令行：

```bash
cd naiwa-app/android
./gradlew assembleDebug
```

### 7. 找到APK文件

构建成功后，APK文件位于：
- **调试版本**: `naiwa-app/android/app/build/outputs/apk/debug/app-debug.apk`
- **发布版本**: `naiwa-app/android/app/build/outputs/apk/release/app-release.apk`

## 应用信息

- **应用名称**: 奶娃
- **包名**: com.naiwa.frog
- **版本**: 1.0.0

## 功能特点

- 视频播放功能（5个视频）
- 跑酷小游戏
- 触摸和键盘双重控制
- 本地存储最高分

## 网络要求

构建APK需要能够访问以下资源：
- Google Maven仓库 (dl.google.com)
- Maven Central
- Gradle分发包

如果在中国大陆，建议配置Gradle使用阿里云镜像。

## 故障排除

### 问题：Gradle下载超时
**解决方案**：配置 Gradle 使用国内镜像

编辑 `naiwa-app/android/build.gradle`，将仓库配置改为：

```gradle
repositories {
    maven { url 'https://maven.aliyun.com/repository/google' }
    maven { url 'https://maven.aliyun.com/repository/central' }
    google()
    mavenCentral()
}
```

### 问题：JAVA_HOME未设置
**解决方案**：
```bash
export JAVA_HOME=/path/to/jdk
export ANDROID_HOME=/path/to/android-sdk
```

## 测试应用

1. 将APK文件传输到Android手机
2. 在手机上启用"安装未知来源应用"
3. 点击APK文件安装
4. 打开应用，开始使用
