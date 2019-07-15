cmake_minimum_required(VERSION 3.8)
set(This GUI)

project(${This} C CXX)

get_directory_property(ParentDirectory PARENT_DIRECTORY)

if(ParentDirectory STREQUAL "")
    
    if(MSVC)
        option(RUNTIME_STATIC_LINKAGE "Link with runtime library statically" OFF)
    endif(MSVC)

    if(MSVC AND RUNTIME_STATIC_LINKAGE)
        foreach(flag
            CMAKE_C_FLAGS
            CMAKE_CXX_FLAGS
            CMAKE_C_FLAGS_DEBUG
            CMAKE_CXX_FLAGS_DEBUG
            CMAKE_C_FLAGS_RELEASE
            CMAKE_CXX_FLAGS_RELEASE
            CMAKE_C_FLAGS_MINSIZEREL
            CMAKE_CXX_FLAGS_MINSIZEREL
            CMAKE_C_FLAGS_RELWITHDEBINFO
            CMAKE_CXX_FLAGS_RELWITHDEBINFO
        )
            if(${flag} MATCHES "/MD")
                string(REGEX REPLACE "/MD" "/MT" ${flag} "${${flag}}")
            endif(${flag} MATCHES "/MD") 
        endforeach(flag)
    endif(MSVC AND RUNTIME_STATIC_LINKAGE)

    set_property(GLOBAL PROPERTY USE_FOLDERS ON)

    set(CMAKE_SKIP_BUILD_RPATH FALSE)
    set(CMAKE_BUILD_WITH_INSTALL_RPATH TRUE)
    if(APPLE)
        set(CMAKE_INSTALL_RPATH "@loader_path")
    elseif(UNIX)
        set(CMAKE_INSTALL_RPATH "\$ORIGIN")
    endif()

    set(CMAKE_DEBUG_POSTFIX "")

    add_definitions(-D_CRT_SECURE_NO_WARNINGS -D_SCL_SECURE_NO_WARNINGS)

    # Specify where to find external libraries.
    # set(variable "${CMAKE_CURRENT_SOURCE_DIR}/${libPath}")
    # Examples:
    # set(SFML   "${CMAKE_CURRENT_SOURCE_DIR}/vendor/SFML")
    # set(SPDLOG "${CMAKE_CURRENT_SOURCE_DIR}/Engine/vendor/spdlog")
    # set(GLFW   "${CMAKE_CURRENT_SOURCE_DIR}/Engine/vendor/GLFW")

    # All other libraries can be pulled in without further configuration.    
    
    add_subdirectory(GUI/vendor)

endif(ParentDirectory STREQUAL "")

# Add subdirectories from this repository.

add_subdirectory(GUI)

set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_CURRENT_BINARY_DIR})