#easy HelloWorld cmake
cmake_minimum_required(VERSION 3.2)

#project(helloworld)
project(helloworld VERSION 0.0.$ENV{TRAVIS_BUILD_NUMBER})
add_executable(helloworld main.cpp)


configure_file(version.h.in version.h)
#
add_library(helloworldLib lib.cpp)
target_include_directories(helloworldLib
    PRIVATE "${CMAKE_BINARY_DIR}"
)
target_link_libraries(helloworld PRIVATE
    helloworldLib)
if (MSVC)
    target_compile_options(helloworld PRIVATE
        /W4
    )
    target_compile_options(helloworldLib PRIVATE
        /W4
    )
#    target_compile_options(test_version PRIVATE
#        /W4
#    )
else ()
    target_compile_options(helloworld PRIVATE
        -Wall -Wextra -pedantic -Werror
    )
    target_compile_options(helloworldLib PRIVATE
        -Wall -Wextra -pedantic -Werror
    )
#    target_compile_options(test_version PRIVATE
#        -Wall -Wextra -pedantic -Werror
#    )
endif()
install(TARGETS helloworld RUNTIME DESTINATION bin)
set(CPACK_GENERATOR DEB)
set(CPACK_PACKAGE_VERSION_MAJOR "${PROJECT_VERSION_MAJOR}")
set(CPACK_PACKAGE_VERSION_MINOR "${PROJECT_VERSION_MINOR}")
set(CPACK_PACKAGE_VERSION_PATCH "${PROJECT_VERSION_PATCH}")

set(CPACK_PACKAGE_CONTACT example@example.com)

include(CPack)
