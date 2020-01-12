#easy HelloWorld cmake
cmake_minimum_required(VERSION 3.2)

#project(helloworld)
project(helloworld VERSION 0.0.$ENV{TRAVIS_BUILD_NUMBER})
add_executable(helloworld main.cpp)
configure_file(version.h.in version.h)
#add_library(helloworldLib lib.cpp)
set(CPACK_GENERATOR DEB)

set(CPACK_PACKAGE_VERSION_MAJOR "${PROJECT_VERSION_MAJOR}")
set(CPACK_PACKAGE_VERSION_MINOR "${PROJECT_VERSION_MINOR}")
set(CPACK_PACKAGE_VERSION_PATCH "${PROJECT_VERSION_PATCH}")

set(CPACK_PACKAGE_CONTACT example@example.com)

include(CPack)
