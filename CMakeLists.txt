cmake_minimum_required(VERSION 3.15)
project(RBK360)

# Options
option(USE_OPENXINPUT
    "Use the modified OpenXInput library instead of standard XInput."
    ON
)

# Set up executable
add_executable(RBK360
    "source/main.cpp"
)

list(APPEND LIBS
    mincore
    WindowsApp
)

list(APPEND HEADERS
    "source/"
)

if(USE_OPENXINPUT)
    add_subdirectory(
        "OpenXinput/"
    )

    list(APPEND LIBS
        Xinput1_4
    )
    
    list(APPEND HEADERS
        "OpenXinput/src/"
    )
endif()

target_link_libraries(RBK360
    PUBLIC
    ${LIBS}
)

target_include_directories(RBK360
    PUBLIC
    ${HEADERS}
)

target_compile_definitions(RBK360
    PUBLIC
    $<$<BOOL:${USE_OPENXINPUT}>:RBK360_USE_OPENXINPUT>
)
