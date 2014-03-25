cmake_minimum_required(VERSION 2.8)

project(HELLOLIB)

add_subdirectory(src)
set(EXECUTABLE_OUTPUT_PATH ${PROJECT_BINARY_DIR}/bin)
set(LIBRARY_OUTPUT_PATH ${PROJECT_BINARY_DIR}/lib)

add_library(hello_share SHARED ${SRC_LIST})
set_target_properties(hello_share PROPERTIES OUTPUT_NAME "hello")
set_target_properties(hello_share PROPERTIES CLEAN_DIRECT_OUTPUT 1)
set_target_properties(hello_share PROPERTIES
  VERSION 1.2 SOVERSION 1)

add_library(hello_static STATIC ${SRC_LIST})
set_target_properties(hello_static PROPERTIES OUTPUT_NAME "hello")
set_target_properties(hello_static PROPERTIES CLEAN_DIRECT_OUTPUT 1)

# install
if(CMAKE_INSTALL_PREFIX_INITIALIZED_TO_DEFAULT)
  set(CMAKE_INSTALL_PREFIX "./install"
      CACHE PATH "hello install prefix" FORCE)
endif(CMAKE_INSTALL_PREFIX_INITIALIZED_TO_DEFAULT)
message(STATUS "INSTALL PREFIX " ${CMAKE_INSTALL_PREFIX})
install(TARGETS hello_share hello_static
        RUNTIME DESTINATION bin
        LIBRARY DESTINATION lib
        ARCHIVE DESTINATION lib)
install(FILES src/hello.hpp DESTINATION include/hello)
