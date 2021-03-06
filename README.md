# ionic-android-builder:1.0
Docker image include Android SDK for building Ionic framework application.

## About this project
In my work, I want to build the android application develop by ionic framework via [gitlab-runner](https://gitlab.com/gitlab-org/gitlab-runner) with Docker driver.

## Example `.gitlab-ci` file
```Dockerfile
build:
  image: josefd8/ionic-android-builder:1.0
  script:
    - npm install
    - mkdir www
    - yes | /opt/android-sdk/tools/bin/sdkmanager --licenses || true
    - ionic cordova build android
  artifacts:
    paths:
    - platforms/android/build/outputs/apk/*.apk
```
## Extra helper command
If you want to run or build the ionic project in computer but doesn't have Android Studio, Android SDK or Ionic Framework and this computer installed Docker. You can use helper command  

- Restore npm package
```
docker run --rm -v $(pwd):/ionicapp josefd8/ionic-android-builder:1.0 npm install
```
- Preview Ionic web app in your web browser
```
docker run --rm -v $(pwd):/ionicapp -p 8100:8100 josefd8/ionic-android-builder:1.0 ionic serve
```
- Build android apk output file
```
docker run --rm -v $(pwd):/ionicapp josefd8/ionic-android-builder:1.0 ionic cordova build android
```

## ADB Support
```
docker run --privileged -v /dev/bus/usb:/dev/bus/usb -P -v $(pwd):/ionicapp josefd8/ionic-android-builder:1.0 /opt/android-sdk/platform-tools/adb devices
```
