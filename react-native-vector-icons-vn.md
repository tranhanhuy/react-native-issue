Link: https://react-native-elements.github.io/react-native-elements/docs/

Sau khi install hay link react-native-vector-icons vẫn không thể run project. Sau đây là các bước sửa, có thể giúp project của bạn run được.

# Một số lỗi

> duplicate output file ‘/Volumes/CodeSpace/ReactNative/myapp/ios/build/myapp/Build/Products/Debug-iphonesimulator/myapp.app/MaterialCommunityIcons.ttf’ on task: PhaseScriptExecution [CP] Copy Pods Resources /Volumes/CodeSpace/ReactNative/myapp/ios/build/myapp/Build/Intermediates.noindex/myapp.build/Debug-iphonesimulator/myapp.build/Script-FEAAB8C4F704294882D02001.sh (in target ‘myapp’ from project ‘myapp’)

> Build system information
warning: The iOS Simulator deployment target is set to 7.0, but the range of supported deployment target versions for this platform is 8.0 to 12.2.99. (in target 'BVLinearGradient')

> Build system information
warning: The iOS Simulator deployment target is set to 4.3, but the range of supported deployment target versions for this platform is 8.0 to 12.2.99. (in target 'nanopb')

> Build system information
warning: The iOS Simulator deployment target is set to 7.0, but the range of supported deployment target versions for this platform is 8.0 to 12.2.99. (in target 'GTMSessionFetcher')

> Unrecognized font family 'Ionicons'

> unrecognized font family 'fontawesome'


# 1. Mở Podfile của iOS 

Thay thế
```
post_install do |installer|
  flipper_post_install(installer)
end
```

Thành 
```
post_install do |installer|
  flipper_post_install(installer)
  installer.pods_project.targets.each do |t|
    t.build_configurations.each do |config|
        config.build_settings['IPHONEOS_DEPLOYMENT_TARGET'] = '9.0'
    end
  end
end
```  
  
# 2. Xoá resources bị trùng (Cụ thể ở đây là các tập tin font)
Mở project bằng xcode, xem Targets > Build Phases như hình sau. Nếu có như hình thì hãy remove các tập tin .ttf. Vì ở [CP] Copy Pods Resources đã thực hiện việc sao chép các file đó rồi.

![alt text](https://github.com/tranhanhuy/react-native-issue/blob/master/images/react-native-vector-icons-1.png "Xoá Resources")

# Kết thúc
Bây giờ bạn hãy thực hiện run lại xem ra sao. Nếu không được, bạn hãy post issue để cungf giải quyết.
