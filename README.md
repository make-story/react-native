# react-native

ReactNative 테스트

`study.git/프론트/ReactNative/환경구축.md` 내용 참고!

## React Native IOS 실행

`애플 M2 탑재된 맥OS의 경우에는 npm run ios 명령을 실행하기 전에 다음 작업을 수행`해야 합니다.

VSCode 에서 ios/Podfile 열고,

```
# Note that if you have use_frameworks! enabled, Flipper will not work and
# you should disable the next line.
```

위 주석을 찾아 다음 라인의 코드를 주석처리 합니다. (Flipper)

다음으로 터미널에서 프로젝트 내부의 ios 디렉토리로 이동한 뒤, ios 에서 사용하는 라이브러리를 설치

```bash
$ cd ios
$ pod install
$ cd ../
$ npm run ios
```

또는

```bash
$ cd ios
$ rm -rf Pods
$ rm -rf Podfile.lock
$ pod install
```

1. Xcode를 프로젝트명.xcworkspace 로 열어줍니다. (예: react-native.git/app/ios/app.xcworkspace)
2. Product > Clean Build Folder 를 실행합니다.
3. ▶︎ 를 눌러 실행합니다.

또는

homebrew 등으로 관련 도구(Node.js 또는 NVM 등)을 설치하면서,
ios 폴더 내부 NVM 버전세팅이 돌아가는 코드의 문제가 있을 수 있음.
이 경우, 'npx react-native init app' CLI 명령으로 프로젝트 다시 생성

https://reactnative.dev/docs/environment-setup?platform=ios&package-manager=yarn#optional-using-a-specific-version-or-template

또는

공식페이지 가이드에 따라 진행  
iOS에 문제가 있는 경우 다음을 실행하여 종속성을 다시 설치해 보세요.

https://reactnative.dev/docs/environment-setup?platform=ios&package-manager=yarn#creating-a-new-application

- 'cd ios' 폴더로 이동합니다.
- 'bundle install' 번들러를 설치
- 'bundle exec pod install' CocoaPods 에서 관리하는 iOS 종속성을 설치

```
Run instructions for Android:
• Have an Android emulator running (quickest way to get started), or a device connected.
• cd "react-native.git/app" && npx react-native run-android

Run instructions for iOS:
• cd "react-native.git/app/ios"

    • Install Cocoapods
      • bundle install # you need to run this only once in your project.
      • bundle exec pod install
      • cd ..

    • npx react-native run-ios
    - or -
    • Open app/ios/app.xcodeproj in Xcode or run "xed -b ios"
    • Hit the Run button

Run instructions for macOS:
• See https://aka.ms/ReactNativeGuideMacOS for the latest up-to-date instructions.
```
