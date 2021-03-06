project (mutexpp)
cmake_minimum_required (VERSION 2.6)

include(${CMAKE_BINARY_DIR}/conanbuildinfo.cmake)
conan_basic_setup()
set(CMAKE_SKIP_RPATH OFF)

set(CMAKE_CXX_FLAGS "-g -Wall -std=c++11")

set(CMAKE_THREAD_PREFER_PTHREAD TRUE)

find_package(Threads)

if(CMAKE_USE_PTHREADS_INIT)
    set(CMAKE_C_FLAGS ${CMAKE_C_FLAGS} "-pthread")
endif()

file(GLOB APP_SRC ./src/*.cpp)

get_filename_component(APP_HEADERS_PATH ./include ABSOLUTE)

include_directories(mutexpp ${APP_HEADERS_PATH} ${CONAN_INCLUDE_DIRS})
link_directories(${CONAN_LIB_DIRS})

add_executable(mutexpp ${APP_SRC})

target_link_libraries(mutexpp ${CONAN_LIBS})

set_target_properties(mutexpp PROPERTIES XCODE_ATTRIBUTE_CLANG_CXX_LANGUAGE_STANDARD c++0x)
set_target_properties(mutexpp PROPERTIES XCODE_ATTRIBUTE_CLANG_CXX_LIBRARY libc++)
