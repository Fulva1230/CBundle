cmake_minimum_required(VERSION 3.20)

project(CBundle)

function(cbundle_deploy target resources_dir search_path bundle_dir)
    get_target_property(target_exe ${target} OUTPUT_NAME)
    configure_file(cmake/bundle.cmake.in bundle.cmake)
endfunction()

add_executable(Test test.cpp)

cbundle_deploy(Test "" "" "")