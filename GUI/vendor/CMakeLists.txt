cmake_minimum_required(VERSION 3.8)

set(This GUI)

set(HEADERS
    include/
)

set(SOURCES
    src/main.cpp
)

add_executable(${This} ${SOURCES} ${HEADERS})

