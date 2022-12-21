# Building the project
1. Fetch submodule dependencies `git submodule update --init --recursive`
2. `cmake -G Xcode -DCMAKE_TOOLCHAIN_FILE=third_party/ios-cmake/ios.toolchain.cmake -DPLATFORM=OS64 -DDEPLOYMENT_TARGET=15.0 -DENABLE_BITCODE=0 -S . -B cmake-build-release`
3. `cd cmake-build-release`
4. `bundler install`
5. Build:
   - `bundle exec fastlane ios beta` - this will fail to build 💥
   - `xcodebuild -project CMakeFastlaneWebpTest.xcodeproj archive -target CMakeFastlaneWebpTest  -configuration Release` - this will succeed ✅ Rerunning previous command will now also succeed.