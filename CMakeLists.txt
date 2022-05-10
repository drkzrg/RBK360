cmake_minimum_required(VERSION 3.15)
project(RBK360)

# Options
option(USE_OPENXINPUT
    "Use the modified OpenXInput library instead of standard XInput."
    ON
)

# Source files
list(APPEND EXE
    "source/main.cpp"
)

# Libraries to use
list(APPEND LIBS
)

# Header file locations
list(APPEND HEADERS
    "source/"
)

# Compile definitions
list(APPEND DEFS
)

# USE_OPENXINPUT option
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

    list(APPEND DEFS
        RBK360_USE_OPENXINPUT
    )
endif()

# Set up executable
add_executable(RBK360 ${EXE})
target_link_libraries(RBK360 PUBLIC ${LIBS})
target_include_directories(RBK360 PUBLIC ${HEADERS})
target_compile_definitions(RBK360 PUBLIC ${DEFS})
