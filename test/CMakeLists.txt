cmake_minimum_required(VERSION 3.15 FATAL_ERROR)
project(
    testCMakeLibs
    VERSION 0.1.0.0
    LANGUAGES CXX)

include(GNUInstallDirs)
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY
    "${CMAKE_BINARY_DIR}/${CMAKE_INSTALL_BINDIR}")
set(CMAKE_LIBRARY_OUTPUT_DIRECTORY
    "${CMAKE_BINARY_DIR}/${CMAKE_INSTALL_LIBDIR}")
set(CMAKE_ARCHIVE_OUTPUT_DIRECTORY
    "${CMAKE_BINARY_DIR}/${CMAKE_INSTALL_LIBDIR}")

add_subdirectory(Alib)
add_subdirectory(Blib)
#add_subdirectory(test)

add_executable(test test/main.cpp) # ${CMAKE_CURRENT_SOURCE_DIR}/include/test_header.
                              # cpp)

target_link_libraries(test PUBLIC Alib::Alib)
#target_include_directories(test PUBLIC ${CMAKE_SOURCE_DIR}/include)
# add_dependencies(test Alib::Alib)
# add_dependencies(test Blib::Blib)

install(TARGETS test
	EXPORT ${PROJECT_NAME}
	DESTINATION bin)