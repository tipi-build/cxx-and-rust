cmake_minimum_required(VERSION 3.17.0)
project(cxx-and-rust VERSION "0.0.1")
enable_testing()

add_subdirectory(contrib/corrosion)
set(CMAKE_MODULE_PATH "${CMAKE_CURRENT_LIST_DIR}/contrib/sanitizers-cmake/cmake/" ${CMAKE_MODULE_PATH})
find_package(Sanitizers MODULE REQUIRED)


# Import targets defined in a package or workspace manifest `Cargo.toml` file
corrosion_import_crate(MANIFEST_PATH ${CMAKE_CURRENT_SOURCE_DIR}/rust/Cargo.toml)
corrosion_add_cxxbridge(cxxbridge-cpp CRATE cxxbridge-crate MANIFEST_PATH rust FILES lib.rs)
add_sanitizers(cxxbridge-cpp)

add_executable(cxxbridge-exe main.cpp)
add_sanitizers(cxxbridge-exe)
target_link_libraries(cxxbridge-exe PUBLIC cxxbridge-cpp)