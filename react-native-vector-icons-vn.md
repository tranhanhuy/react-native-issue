Link: https://react-native-elements.github.io/react-native-elements/docs/

Sau khi install hay link react-native-vector-icons vẫn không thể run project. Sau đây là các bước sửa, có thể giúp project của bạn run được.

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

![alt text](https://miro.medium.com/max/700/1*qFe_NrpBd55-RI8U7lmzdA.png "Xoá Resources")

# Kết thúc
Bây giờ bạn hãy thực hiện run lại xem ra sao. Nếu không được, bạn hãy post issue để cungf giải quyết.
