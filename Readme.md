# Bazel:
`cd PerformanceTest_Bazel`

`bazel run //:xcodeproj`

### Environment
- bazel 6.0.0
- openjdk 11.0.11 2021-04-20
- macOS 13.1

# Xcode build command:

```
time xcodebuild -project 'PerformanceTest_Xcode.xcodeproj' \
-scheme 'PerformanceTest_Xcode' \
-configuration Debug \
-destination 'platform=iOS Simulator,name=iPhone 14' \
-derivedDataPath build
```

# Buck:
`./buck build //App:PerformanceTestApp`