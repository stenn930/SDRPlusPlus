cmake_minimum_required(VERSION 3.13)
project(fobosagilesdr_source)

file(GLOB SRC "src/*.cpp" "src/*.c")

include(${SDRPP_MODULE_CMAKE})

if (MSVC)
    # Lib path
    target_link_directories(fobosagilesdr_source PRIVATE "C:/Program Files/RigExpert/Fobos/lib/")
    target_include_directories(fobosagilesdr_source PRIVATE "C:/Program Files/RigExpert/Fobos/include/")
    target_link_libraries(fobosagilesdr_source PRIVATE fobos)
else (MSVC)
    find_package(PkgConfig)

    pkg_check_modules(LIBUSB REQUIRED libusb-1.0)

    target_include_directories(fobosagilesdr_source PRIVATE ${LIBUSB_INCLUDE_DIRS})
    target_link_directories(fobosagilesdr_source PRIVATE ${LIBUSB_LIBRARY_DIRS})
    target_link_libraries(fobosagilesdr_source PRIVATE ${LIBUSB_LIBRARIES})
endif ()