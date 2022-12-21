cmake_minimum_required(VERSION 3.23)
project(CMakeFastlaneWebpTest)

set(CMAKE_CXX_STANDARD 14)

add_executable(CMakeFastlaneWebpTest src/main.cpp)

# Skip building of unused webp tools which fail for me under ios:
set(WEBP_BUILD_ANIM_UTILS OFF)
set(WEBP_BUILD_CWEBP OFF)
set(WEBP_BUILD_DWEBP OFF)
set(WEBP_BUILD_GIF2WEBP OFF)
set(WEBP_BUILD_IMG2WEBP OFF)
set(WEBP_BUILD_VWEBP OFF)
set(WEBP_BUILD_WEBPINFO OFF)
set(WEBP_BUILD_WEBPMUX OFF)
set(WEBP_BUILD_EXTRAS OFF)
set(WEBP_BUILD_WEBP_JS OFF)
add_subdirectory(third_party/libwebp EXCLUDE_FROM_ALL)
target_link_libraries(CMakeFastlaneWebpTest PRIVATE webpdecoder webpdemux)
include_directories(SYSTEM ${CMAKE_SOURCE_DIR}/third_party/libwebp/src)

configure_file(${CMAKE_SOURCE_DIR}/fastlane/Appfile ${CMAKE_BINARY_DIR}/fastlane/Appfile COPYONLY)
configure_file(${CMAKE_SOURCE_DIR}/fastlane/Fastfile ${CMAKE_BINARY_DIR}/fastlane/Fastfile COPYONLY)
configure_file(${CMAKE_SOURCE_DIR}/Gemfile ${CMAKE_BINARY_DIR}/Gemfile COPYONLY)
configure_file(${CMAKE_SOURCE_DIR}/Gemfile.lock ${CMAKE_BINARY_DIR}/Gemfile.lock COPYONLY)

set_target_properties(CMakeFastlaneWebpTest PROPERTIES
        XCODE_ATTRIBUTE_IPHONEOS_DEPLOYMENT_TARGET ${DEPLOYMENT_TARGET}
        MACOSX_BUNDLE TRUE
        MACOSX_BUNDLE_INFO_PLIST ${CMAKE_SOURCE_DIR}/src/iOS-Info.plist.in
        MACOSX_BUNDLE_GUI_IDENTIFIER com.dbotha.CMakeFastlaneWebpTest
        MACOSX_BUNDLE_BUNDLE_NAME CMakeFastlaneWebpTest
        MACOSX_BUNDLE_BUNDLE_VERSION "0.1"
        MACOSX_BUNDLE_SHORT_VERSION_STRING "0.1"
        )

set_xcode_property(CMakeFastlaneWebpTest PRODUCT_BUNDLE_IDENTIFIER "com.dbotha.CMakeFastlaneWebpTest" All)
set_xcode_property(CMakeFastlaneWebpTest CODE_SIGN_IDENTITY "iPhone Developer" All)
set_xcode_property(CMakeFastlaneWebpTest DEVELOPMENT_TEAM "GFP63373B2" All)