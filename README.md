### Continuous Integration with CircleCI

[![CircleCI](https://circleci.com/gh/WeRockStar/AndroidCircleCI.svg?style=svg)](https://circleci.com/gh/WeRockStar/AndroidCircleCI)

###### - Circle CI script (circle.yml)
```yaml
general:
    artifacts:
        - /home/ubuntu/{YOUR_PROJECT_NAME}/app/build/outputs/apk/

machine:
    environment:
        ANDROID_HOME: /usr/local/android-sdk-linux

dependencies:
    pre:
        - echo y | android update sdk --no-ui --all --filter tools,platform-tools,android-24,extra-google-m2repository,extra-android-support
        - echo y | android update sdk --no-ui --all --filter build-tools-24.0.3
    cache_directories:
        - /usr/local/android-sdk-linux/tools
        - /usr/local/android-sdk-linux/build-tools/24.0.3
test:
    override:
        - (./gradlew test):
            timeout: 520
        - cp -r app/build/reports $CIRCLE_ARTIFACTS
```