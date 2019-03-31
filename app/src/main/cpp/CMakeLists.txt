cmake_minimum_required(VERSION 3.4.1)

set(distribution_DIR ${CMAKE_CURRENT_SOURCE_DIR}/../../../../distributions)

add_library(lib_ncnn STATIC IMPORTED)
set_target_properties(lib_ncnn PROPERTIES IMPORTED_LOCATION
        ${distribution_DIR}/ncnn/lib/${ANDROID_ABI}/libncnn.a)

set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=gnu++11")

add_library(face-detect-lib SHARED
            face-detect-lib.cpp)

target_include_directories(face-detect-lib PRIVATE
                           ${distribution_DIR}/ncnn/include)

target_link_libraries(face-detect-lib
                      android
                      lib_ncnn
                      jnigraphics
                      log)