cmake_minimum_required(VERSION 3.0)

project(finn)

enable_language(Fortran)

find_package(MKL CONFIG REQUIRED)

message(STATUS "${MKL_IMPORTED_TARGETS}")

file(GLOB SRC_FILES ${PROJECT_SOURCE_DIR}/src/*.f90)

add_executable(${PROJECT_NAME} ${SRC_FILES})

target_compile_options(${PROJECT_NAME} PUBLIC $<TARGET_PROPERTY:MKL::MKL,INTERFACE_COMPILE_OPTIONS>)
target_include_directories(${PROJECT_NAME} PUBLIC $<TARGET_PROPERTY:MKL::MKL,INTERFACE_INCLUDE_DIRECTORIES>)
target_link_libraries(${PROJECT_NAME} PUBLIC $<LINK_ONLY:MKL::MKL>)
