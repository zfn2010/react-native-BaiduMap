# react-native-BaiduMap

从原作者 fork 下来，原项目很久没维护了，故新开一个模块用于维护百度地图上的 RN 使
用。</br>原项目 https://github.com/lovebing/react-native-baidu-map </br>目前在
android 端进行了测试升级，ios 待跟进

# react-native-BaiduMap [![npm version](https://img.shields.io/npm/v/react-native-BaiduMap.svg?style=flat)](https://www.npmjs.com/package/react-native-BaiduMap)

Baidu Map SDK modules and view for React Native(Android & IOS), support react
native 0.47+

百度地图 React Native 模块，支持 react native 0.47+

![Android](https://raw.githubusercontent.com/zfn2010/react-native-BaiduMap/master/images/android.jpg)
![IOS](https://raw.githubusercontent.com/zfn2010/react-native-BaiduMap/master/images/ios.jpg)

### Install 安装

    npm install react-native-baidumap --save

### Import 导入

#### Android Studio

* settings.gradle `include ':react-native-BaiduMap'
  project(':react-native-BaiduMap').projectDir = new File(settingsDir,
  '../node_modules/react-native-BaiduMap/android')`

* build.gradle `compile project(':react-native-baidumap')`

* MainApplication`new BaiduMapPackage(getApplicationContext())`
* AndroidMainifest.xml `<meta-data android:name="com.baidu.lbsapi.API_KEY"
  android:value="xx"/>`

#### Xcode

* Project navigator->Libraries->Add Files to 选择
  react-native-BaiduMap/ios/RCTBaiduMap.xcodeproj
* Project navigator->Build Phases->Link Binary With Libraries 加入
  libRCTBaiduMap.a
* Project navigator->Build Settings->Search Paths， Framework search paths 添加
  react-native-BaiduMap/ios/lib，Header search paths 添加
  react-native-BaiduMap/ios/RCTBaiduMap
* 添加依赖 , react-native-BaiduMap/ios/lib 下的全部 framwordk，
  CoreLocation.framework 和 QuartzCore.framework、OpenGLES.framework 、
  SystemConfiguration.framework、CoreGraphics.framework 、
  Security.framework、libsqlite3.0.tbd （ xcode7 以前为 libsqlite3.0.dylib）、
  CoreTelephony.framework 、libstdc++.6.0.9.tbd （ xcode7 以前为
  libstdc++.6.0.9.dylib）
* 添加 BaiduMapAPI_Map.framework/Resources/mapapi.bundle

* 其它一些注意事项可参考百度地图 LBS 文档

##### AppDelegate.m init 初始化

    #import "RCTBaiduMapViewManager.h"
    - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions
    {
        ...
        [RCTBaiduMapViewManager initSDK:@"api key"];
        ...
    }

### Usage 使用方法

    import { MapView, MapTypes, MapModule, Geolocation } from 'react-native-baidumap'

#### MapView Props 属性

| Name                    |  Type  |  Default  | Extra                                  |
| ----------------------- | :----: | :-------: | -------------------------------------- |
| zoomControlsVisible     |  bool  |   true    | Android only                           |
| trafficEnabled          |  bool  |   false   |
| baiduHeatMapEnabled     |  bool  |   false   |
| mapType                 | number |     1     |
| zoom                    | number |    10     |
| center                  | object |   null    | {latitude: 0, longitude: 0}            |
| marker                  | object |   null    | {latitude: 0, longitude: 0, title: ''} |
| markers                 | array  |    []     | [marker, maker]                        |
| onMapStatusChangeStart  |  func  | undefined | Android only                           |
| onMapStatusChange       |  func  | undefined |
| onMapStatusChangeFinish |  func  | undefined | Android only                           |
| onMapLoaded             |  func  | undefined |
| onMapClick              |  func  | undefined |
| onMapDoubleClick        |  func  | undefined |
| onMarkerClick           |  func  | undefined |
| onMapPoiClick           |  func  | undefined |

#### MapModule Methods (Deprecated)

    setMarker(double lat, double lng)
    setMapType(int mapType)
    moveToCenter(double lat, double lng, float zoom)
    Promise reverseGeoCode(double lat, double lng)
    Promise reverseGeoCodeGPS(double lat, double lng)
    Promise geocode(String city, String addr),
    Promise getCurrentPosition()

#### Geolocation Methods

| Method                                            | Result                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| ------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| Promise reverseGeoCode(double lat, double lng)    | `{"address": "", "province": "", "cityCode": "", "city": "", "district": "", "streetName": "", "streetNumber": ""}`                                                                                                                                                                                                                                                                                                                              |
| Promise reverseGeoCodeGPS(double lat, double lng) | `{"address": "", "province": "", "cityCode": "", "city": "", "district": "", "streetName": "", "streetNumber": ""}`                                                                                                                                                                                                                                                                                                                              |
| Promise geocode(String city, String addr)         | {"latitude": 0.0, "longitude": 0.0}                                                                                                                                                                                                                                                                                                                                                                                                              |
| Promise getCurrentPosition()                      | IOS: `{"latitude": 0.0, "longitude": 0.0, "address": "", "province": "", "cityCode": "", "city": "", "district": "", "streetName": "", "streetNumber": ""}` Android: `{"latitude": 0.0, "longitude": 0.0, "direction": -1, "altitude": 0.0, "radius": 0.0, "address": "", "countryCode": "", "country": "", "province": "", "cityCode": "", "city": "", "district": "", "street": "", "streetNumber": "", "buildingId": "", "buildingName": ""}` |

### TODOList

* [x] 实现 android 端地图标记图片自定义（注：需要在 drawble 下放对于图片资源）
* [] ios 端地图标记图片自定义
