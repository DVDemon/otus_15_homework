cmake_minimum_required(VERSION 3.2)

if($ENV{TRAVIS_BUILD_NUMBER})
 project(15_homework VERSION 0.0.$ENV{TRAVIS_BUILD_NUMBER})
else()
 project(15_homework VERSION 0.0.3)
endif()

#SET(CMAKE_CXX_COMPILER /usr/local/Cellar/gcc/9.2.0_2/bin/c++-9)

find_package(Threads)


add_executable(kkmeans kkmeans_ex.cpp)

set_target_properties(kkmeans PROPERTIES CXX_STANDARD 14 CXX_STANDARD_REQUIRED ON)

target_include_directories(kkmeans PRIVATE "${CMAKE_BINARY_DIR}")
target_link_libraries(kkmeans PRIVATE ${CMAKE_THREAD_LIBS_INIT} dlib lapack blas)

install(TARGETS kkmeans RUNTIME DESTINATION bin)

set(CPACK_GENERATOR DEB)
set(CPACK_PACKAGE_VERSION_MAJOR "${PROJECT_VERSION_MAJOR}")
set(CPACK_PACKAGE_VERSION_MINOR "${PROJECT_VERSION_MINOR}")
set(CPACK_PACKAGE_VERSION_PATCH "${PROJECT_VERSION_PATCH}")
set(CPACK_PACKAGE_CONTACT ddzuba@yandex.ru)
include(CPack)

