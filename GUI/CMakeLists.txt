cmake_minimum_required(VERSION 3.8)

set(This GUI)

set(HEADERS
#    include/
)

set(SOURCES
    src/main.cpp
)

# How to add a directory to include path: 
# include_directories(${variable}/include)

# How to add a directory to link path: 
# link_directories(${variable}/lib)

# How to add compilation definitions:
# add_compile_definitions(difinition)

# executable
add_executable(${This} ${SOURCES} ${HEADERS})

# library
# add_library(${This} STATIC ${SOURCES} ${HEADERS})

# target_link_libraries(${This} PUBLIC
#    GLAD
#    GLEW
#    GLFW
#    ImGUI
# )

target_include_directories(${This} PUBLIC include)

set_target_properties(${This} PROPERTIES 
    FOLDER Application
)