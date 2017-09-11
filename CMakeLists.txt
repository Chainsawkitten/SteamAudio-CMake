cmake_minimum_required(VERSION 3.1.0)

project(SteamAudio)

# Windows libraries.
if(WIN32)
    # 64-bit.
    if(CMAKE_SIZEOF_VOID_P EQUAL 8)
        set(SteamAudio_LIBRARY "${CMAKE_CURRENT_SOURCE_DIR}/lib/Windows/x64/phonon.lib")
    # 32-bit.
    else()
        set(SteamAudio_LIBRARY "${CMAKE_CURRENT_SOURCE_DIR}/lib/Windows/x86/phonon.lib")
    endif()
# Mac libraries.
elseif(APPLE)
    set(SteamAudio_LIBRARY "${CMAKE_CURRENT_SOURCE_DIR}/lib/OSX/libphonon.dylib")
# Android libraries.
elseif(ANDROID)
    set(SteamAudio_LIBRARY "${CMAKE_CURRENT_SOURCE_DIR}/lib/Android/libphonon.so")
# Linux libraries.
elseif(UNIX)
    # 64-bit.
    if(CMAKE_SIZEOF_VOID_P EQUAL 8)
        set(SteamAudio_LIBRARY "${CMAKE_CURRENT_SOURCE_DIR}/lib/Linux/x64/libphonon.so")
    # 32-bit.
    else()
        set(SteamAudio_LIBRARY "${CMAKE_CURRENT_SOURCE_DIR}/lib/Linux/x86/libphonon.so")
    endif()
endif()

add_library(SteamAudio INTERFACE)
target_include_directories(SteamAudio INTERFACE include)
target_link_libraries(SteamAudio INTERFACE ${SteamAudio_LIBRARY})
