DEPLOYMENT_TARGET = '12.0'
platform :ios, DEPLOYMENT_TARGET
use_frameworks!
workspace 'RugbyTest'

def client_pods
  pod 'Apptimize', '~> 3.4.7'
  pod 'JumioMobileSDK/NetverifyBase', '3.9.1'
  pod 'JumioMobileSDK/NetverifyFace+iProov', '3.9.1'
  pod 'JumioMobileSDK/DocumentVerification', '3.9.1'
  pod 'JumioMobileSDK/NetverifyBarcode', '3.9.1'
  pod 'Segment-Amplitude', '~> 3.0.1'
  pod 'segment-appsflyer-ios', '~> 6.3.0'
  pod 'Segment-Apptimize', '~> 0.3.2'
end

target :RugbyTest do
  client_pods
end

post_install do |installer|
  installer.pods_project.targets.each do |target|
    if ['iProov', 'Socket.IO-Client-Swift', 'Starscream'].include? target.name
      target.build_configurations.each do |config|
        config.build_settings['BUILD_LIBRARY_FOR_DISTRIBUTION'] = 'YES'
      end
    end
    target.build_configurations.each do |config|
      config.build_settings['ONLY_ACTIVE_ARCH'] = 'NO'
      config.build_settings["EXCLUDED_ARCHS[sdk=iphonesimulator*]"] = "arm64"
      config.build_settings['IPHONEOS_DEPLOYMENT_TARGET'] = DEPLOYMENT_TARGET
    end
  end
end
