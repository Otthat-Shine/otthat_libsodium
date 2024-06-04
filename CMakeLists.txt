cmake_minimum_required(VERSION 3.18)
project(otthat_libsodium)

set(CMAKE_CXX_STANDARD 17)

add_library(libsodium STATIC IMPORTED GLOBAL)
if (WIN32)
    set_target_properties(libsodium PROPERTIES
            IMPORTED_LOCATION_DEBUG "${CMAKE_CURRENT_SOURCE_DIR}/prebuilt/windows/Debug/libsodium.lib"
            IMPORTED_LOCATION_RELEASE "${CMAKE_CURRENT_SOURCE_DIR}/prebuilt/windows/Release/libsodium.lib"
    )
endif ()

if (ANDROID)
    set_target_properties(libsodium PROPERTIES
            IMPORTED_LOCATION "${CMAKE_CURRENT_SOURCE_DIR}/prebuilt/android/${ANDROID_ABI}/libsodium.a"
    )
endif ()

target_include_directories(libsodium INTERFACE
        "$<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/include>"
        "$<INSTALL_INTERFACE:include>"
)
