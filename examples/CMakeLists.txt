cmake_minimum_required(VERSION 3.10)

if(CMAKE_CURRENT_SOURCE_DIR STREQUAL CMAKE_SOURCE_DIR) # stand-alone
    message("project(My_exmples_libstudxml CXX)")
    project(My_exmples_libstudxml CXX)
else() # reffered by add_subdirectory()
    message(STATUS )
    message(STATUS "${PROJECT_NAME}_exmple_exe:")
endif()


# project(Myexmples)

# Set C++ standard
# set(CMAKE_CXX_STANDARD 20)
# set(CMAKE_CXX_STANDARD_REQUIRED ON)


# Define a macro to list all subdirectories containing *.cxx files
macro(SUBDIRLIST result curdir)
    file(GLOB children RELATIVE ${curdir} ${curdir}/*)
    set(dirlist "")
    foreach(child ${children})
        if(IS_DIRECTORY ${curdir}/${child})
            file(GLOB cxx_files "${curdir}/${child}/*.cxx") # Check for .cxx files in the current subdirectory
            if(cxx_files)  
                list(APPEND dirlist ${child})
            endif()
        endif()
    endforeach()
    set(${result} ${dirlist})
endmacro()
# Use the macro to get all subdirectories 
SUBDIRLIST(SubDir_xs ${CMAKE_CURRENT_SOURCE_DIR})

foreach(dir ${SubDir_xs})
  file(GLOB_RECURSE HEADER_FILES "${dir}/*.hxx")
  file(GLOB_RECURSE SOURCE_FILES "${dir}/*.cxx")

  add_executable(${dir} ${SOURCE_FILES} ${HEADER_FILES})
  target_link_libraries(${dir} libstudxml)
  # add_test(NAME ${dir} COMMAND ${dir})
  set_target_properties(${dir} PROPERTIES RUNTIME_OUTPUT_DIRECTORY "${CMAKE_CURRENT_SOURCE_DIR}/${dir}"
)

endforeach()


# Get all targets in the current directory
get_property(target_names DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR} PROPERTY BUILDSYSTEM_TARGETS)
foreach(target ${target_names})
    get_target_property(target_type ${target} TYPE)
    if(target_type STREQUAL "EXECUTABLE")
        message(STATUS "\t\t${target}")
    endif()
endforeach()
message(STATUS)
