cmake_minimum_required(VERSION 2.8)

project(NEWHELLO)

set(hello_install_dir
  "$ENV{HOME}/dev/cmake/cmake_example/t3/build/install/")

include_directories(BEFORE
  ${hello_install_dir}/include/hello)
link_directories(${hello_install_dir}/lib)

add_executable(main "src/main.cpp")

# static
target_link_libraries(main
  ${hello_install_dir}/lib/libhello.a)

# # share
# target_link_libraries(main hello)