cmake_minimum_required(VERSION 3.27)
project(audioproject)

set(CMAKE_CXX_STANDARD 17)

include(FetchContent)

FetchContent_Declare(
        rtaudio
        GIT_REPOSITORY https://github.com/thestk/rtaudio.git
        GIT_TAG 6.0.1
)

set(RTAUDIO_API_WASAPI ON CACHE BOOL "Enable WASAPI" FORCE)
set(RTAUDIO_API_DS ON CACHE BOOL "Enable DirectSound" FORCE)
set(RTAUDIO_API_ASIO OFF CACHE BOOL "Disable ASIO" FORCE)
set(BUILD_SHARED_LIBS OFF CACHE BOOL "Build static library" FORCE)

FetchContent_MakeAvailable(rtaudio)

add_executable(AudioProject main.cpp)

target_link_libraries(AudioProject rtaudio)

if(WIN32)
    target_link_libraries(AudioProject winmm ole32 ksuser)
    set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -static-libgcc -static-libstdc++")
endif()