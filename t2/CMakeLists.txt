cmake_minimum_required(VERSION 2.8)

project(HELLO)

message(STATUS
        "CURRENT SOURCE dir: " ${CMAKE_CURRENT_SOURCE_DIR})
message(STATUS "BINARY dir: " ${PROJECT_BINARY_DIR})
message(STATUS "SOURCE dir: " ${PROJECT_SOURCE_DIR})

add_subdirectory(src)
set(EXECUTABLE_OUTPUT_PATH ${PROJECT_BINARY_DIR}/bin)
set(LIBRARY_OUTPUT_PATH ${PROJECT_BINARY_DIR}/lib)

add_executable(hello ${SRC_LIST})

# install
if(CMAKE_INSTALL_PREFIX_INITIALIZED_TO_DEFAULT)
  set(CMAKE_INSTALL_PREFIX "./install"
      CACHE PATH "hello install prefix" FORCE)
endif(CMAKE_INSTALL_PREFIX_INITIALIZED_TO_DEFAULT)
message(STATUS "INSTALL PREFIX " ${CMAKE_INSTALL_PREFIX})
install(TARGETS hello
        RUNTIME DESTINATION bin
        LIBRARY DESTINATION lib
        ARCHIVE DESTINATION libstatic)
install(FILES COPYRIGHT README DESTINATION share/doc/cmake/t2)
install(DIRECTORY doc/ DESTINATION share/doc/cmake/t2)
install(PROGRAMS runhello.sh DESTINATION bin)
