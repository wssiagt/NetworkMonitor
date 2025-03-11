# NetworkMonitor

## 项目简介
本项目旨在开发一个 Android 应用，帮助用户实时读取手机的小区驻网信息，并结合 GPS 数据在地图中绘制信号强弱的路线图或热力图，以便用户寻找最佳的移动网络环境。此外，该应用还提供自动化通话功能，并支持详细日志记录。

## 主要功能
1. **驻网小区信息读取**：使用 Android API 获取当前驻网小区的网络信息（支持 SIM1 和 SIM2）。
2. **地图可视化**：
   - 实时在地图上展示信号强弱，支持放大、缩小和定位自身位置。
   - 允许用户筛选不同的网络类型和信号强度，以便更精准地选择打点区域。
   - 支持热力图或不同颜色的标点表示不同的网络环境质量。
3. **通话自动化**：
   - 提供通话脚本配置，包括通话时长、通话间隔、通话次数和接听号码。
   - 允许用户启动和停止自动化通话任务。
   - 记录通话日志，并在任务完成后输出保存路径。
4. **悬浮窗**：
   - 用户可选择启用悬浮窗，显示 SIM1 和 SIM2 的驻网小区信息、GPS 信息。
   - 悬浮窗可自由拖动、缩放，文本排列整齐，避免遮挡主要 UI。
5. **日志功能**：
   - 记录驻网小区、GPS 位置变化、邻近小区信息。
   - 通话日志与驻网小区日志独立存储，通话日志仅在通话任务启动后记录。
   - 日志按照系统时间进行分类存储，提供日志路径提示。

## 应用流程
1. **权限请求**：首次启动时请求必要的系统权限（定位、电话、日志写入）。
2. **首页布局**：
   - **Cell 页面**：显示驻网信息、GPS 定位信息、SIM 运营商、网络类型、是否注册 CA（支持 SIM1 和 SIM2）。
   - **Map 页面**：
     - 显示地图和用户当前位置。
     - 页面顶部显示当前数据卡的网络类型、运营商、小区信息、信号强度。
     - 提供筛选功能（网络类型、信号强度、热力图）。
     - 选择筛选条件后，地图每 3 秒更新一次数据点或热力图。
     - 右上角菜单提供日志开关，并在日志记录结束后提示保存路径。
   - **Call 页面**：
     - 提供通话脚本配置（通话时长、间隔、次数、接听号码）。
     - 启动后自动记录通话日志，停止后自动提示日志保存路径。

## 目录结构
├─app
│  │  .gitignore
│  │  build.gradle.kts
│  │  proguard-rules.pro
│  │  
│  └─src
│      ├─androidTest
│      │  └─java
│      │      └─com
│      │          └─example
│      │              └─networkmonitor
│      │                      ExampleInstrumentedTest.kt
│      │                      
│      ├─main
│      │  │  AndroidManifest.xml
│      │  │  
│      │  ├─java
│      │  │  └─com
│      │  │      └─example
│      │  │          └─networkmonitor
│      │  │              │  MainActivity.kt
│      │  │              │  
│      │  │              ├─database
│      │  │              ├─models
│      │  │              │      CallConfig.kt
│      │  │              │      
│      │  │              ├─services
│      │  │              │      CallAutomationService.kt
│      │  │              │      CellInfoService.kt
│      │  │              │      FloatingWindowService.kt
│      │  │              │      LocationService.kt
│      │  │              │      LoggingService.kt
│      │  │              │      
│      │  │              ├─ui
│      │  │              │  │  CallFragment.kt
│      │  │              │  │  CellFragment.kt
│      │  │              │  │  MapFragment.kt
│      │  │              │  │  
│      │  │              │  └─theme
│      │  │              │          Color.kt
│      │  │              │          Theme.kt
│      │  │              │          Type.kt
│      │  │              │          
│      │  │              └─utils
│      │  │                      DataProcessor.kt
│      │  │                      PermissionsHelper.kt
│      │  │                      
│      │  └─res
│      │      ├─drawable
│      │      │      ic_floating_window_off.xml
│      │      │      ic_floating_window_on.xml
│      │      │      ic_launcher_background.xml
│      │      │      ic_launcher_foreground.xml
│      │      │      
│      │      ├─layout
│      │      │      activity_main.xml
│      │      │      floating_window.xml
│      │      │      fragment_call.xml
│      │      │      fragment_cell.xml
│      │      │      fragment_map.xml
│      │      │      
│      │      ├─mipmap-anydpi
│      │      │      ic_launcher.xml
│      │      │      ic_launcher_round.xml
│      │      │      
│      │      ├─mipmap-hdpi
│      │      │      ic_launcher.webp
│      │      │      ic_launcher_round.webp
│      │      │      
│      │      ├─mipmap-mdpi
│      │      │      ic_launcher.webp
│      │      │      ic_launcher_round.webp
│      │      │      
│      │      ├─mipmap-xhdpi
│      │      │      ic_launcher.webp
│      │      │      ic_launcher_round.webp
│      │      │      
│      │      ├─mipmap-xxhdpi
│      │      │      ic_launcher.webp
│      │      │      ic_launcher_round.webp
│      │      │      
│      │      ├─mipmap-xxxhdpi
│      │      │      ic_launcher.webp
│      │      │      ic_launcher_round.webp
│      │      │      
│      │      ├─values
│      │      │      colors.xml
│      │      │      strings.xml
│      │      │      themes.xml
│      │      │      
│      │      └─xml
│      │              backup_rules.xml
│      │              data_extraction_rules.xml
│      │              
│      └─test
│          └─java
│              └─com
│                  └─example
│                      └─networkmonitor
│                              ExampleUnitTest.kt
│                              
└─gradle
    │  libs.versions.toml
    │  
    └─wrapper
            gradle-wrapper.jar
            gradle-wrapper.properties
            

            

            


## 📌 目录说明
- **`app/src/main/java/com/example/networkmonitor/`**：Kotlin 代码目录。
  - **`MainActivity.kt`**：应用主入口，管理 Fragment 切换。
  - **`ui/`**：存放 UI 相关代码，包括 Cell、Map、Call 三个 Fragment。
  - **`services/`**：后台服务代码，包括驻网信息获取、位置获取、通话自动化、悬浮窗管理、日志管理等。
  - **`utils/`**：工具类，提供权限管理、数据处理等通用功能。

- **`app/src/main/res/`**：资源文件目录。
  - **`layout/`**：存放各个 Fragment 对应的 XML 布局文件。
  - **`values/`**：存放字符串、颜色、样式等资源文件。

- **`AndroidManifest.xml`**：应用权限声明，包括 GPS 访问、电话权限、悬浮窗权限等。

- **`logs/`**：日志文件存储目录，记录驻网小区、GPS 位置变化、通话记录等。

- **`build.gradle.kts`**：Gradle 构建配置文件，管理项目依赖。

## 🎯 开发指南
1. **界面开发**
   - 在 `ui/` 目录下开发 Fragment 并关联到 `MainActivity.kt`。
   - 使用 `layout/` 目录中的 XML 布局文件设计界面。

2. **后台服务**
   - 在 `services/` 目录中编写后台逻辑。
   - 例如 `CellInfoService.kt` 负责获取驻网信息并定期更新。

3. **权限管理**
   - 在 `PermissionsHelper.kt` 中实现动态权限申请。
   - 确保应用运行时获取 `ACCESS_FINE_LOCATION`、`READ_PHONE_STATE` 等必要权限。

4. **日志存储**
   - `LoggingService.kt` 负责写入日志。
   - 日志按照系统时间存储到 `logs/` 目录下。


## 技术栈
- **语言**：Kotlin
- **UI 框架**：Jetpack Compose / XML Layout
- **地图**：Google Maps API
- **数据存储**：Room / SQLite / JSON 日志
- **后台服务**：Foreground Service 处理驻网数据和通话自动化

## 运行环境
- **最低支持 Android 版本**：Android 8.0 (API Level 26)
- **开发工具**：Android Studio Flamingo+
- **依赖项**：
  - Google Maps SDK
  - Jetpack Compose (可选)
  - Android Telephony API
  - GPS Location API
  - Foreground Service

## 权限需求
- `android.permission.ACCESS_FINE_LOCATION` - 获取 GPS 位置
- `android.permission.READ_PHONE_STATE` - 读取 SIM 卡和驻网信息
- `android.permission.CALL_PHONE` - 执行自动拨号
- `android.permission.WRITE_EXTERNAL_STORAGE` - 记录日志
- `android.permission.SYSTEM_ALERT_WINDOW` - 显示悬浮窗
