### Continuous Integration with CircleCI

```yaml
general:
    artifacts:
        - /home/ubuntu/{YOUR_PROJECT_NAME}/app/build/outputs/apk/

machine:
    environment:
        ANDROID_HOME: /usr/local/android-sdk-linux

dependencies:
    pre:
        - echo y | android update sdk --no-ui --all --filter tools,platform-tools,android-23,extra-google-m2repository,extra-android-support
        - echo y | android update sdk --no-ui --all --filter build-tools-24.0.1
    cache_directories:
        - /usr/local/android-sdk-linux/tools
        - /usr/local/android-sdk-linux/build-tools/24.0.1
test:
    override:
        - (./gradlew test):
            timeout: 420
        - cp -r app/build/reports $CIRCLE_ARTIFACTS
```