cmake_minimum_required(VERSION 3.20)

project(CBundle)

#cbundle_deploy(
#        TARGET Test
#        BUNDLE_DIR ${CMAKE_CURRENT_BINARY_DIR}/dist
#        TARGET_EXE_PATH ${CMAKE_CURRENT_BINARY_DIR}/Test.exe
#        DLL_PATH 1 2 3 4 5
#        RESOURCES_PATH 5 6 7 8 9
#)
set(CBundle_DIR CACHE PATH ${CMAKE_CURRENT_LIST_DIR})
function(cbundle_deploy)
    set(oneValueArgs TARGET BUNDLE_DIR TARGET_EXE_PATH )
    set(multiValueArgs DLL_PATH RESOURCES_PATH)
    cmake_parse_arguments(PARSE_ARGV 0 CBUNDLE "" "${oneValueArgs}" "${multiValueArgs}")
    message(VERBOSE "TARGET is ${CBUNDLE_TARGET}")
    message(VERBOSE "BUNDLE_DIR is ${CBUNDLE_BUNDLE_DIR}")
    message(VERBOSE "TARGET_EXE_PATH is ${CBUNDLE_TARGET_EXE_PATH}")
    message(VERBOSE "DLL_PATH is ${CBUNDLE_DLL_PATH}")
    message(VERBOSE "RESOURCES_PATH is ${CBUNDLE_RESOURCES_PATH}")

    configure_file(${CBundle_SOURCE_DIR}/cmake/bundle.cmake.in bundle.cmake @ONLY)
    add_custom_command(TARGET ${CBUNDLE_TARGET} POST_BUILD
            COMMAND cmake -P ${CMAKE_CURRENT_BINARY_DIR}/bundle.cmake
    )
endfunction()