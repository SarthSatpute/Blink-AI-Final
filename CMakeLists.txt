cmake_minimum_required(VERSION 3.26)
include(CMakePrintHelpers)

# Start the project
project(Mousedroid)

# Set output directory for the runtime
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/bin)

# Specify wxWidgets path manually if not found
set(wxWidgets_ROOT_DIR "C:/wxWidgets-3.2.7")
set(wxWidgets_INCLUDE_DIRS "C:/wxWidgets-3.2.7/include")
set(wxWidgets_LIB_DIR "C:/wxWidgets-3.2.7/lib/vc_x64_lib")

# Find wxWidgets
find_package(wxWidgets REQUIRED net gl core base adv)

# Set ASIO path explicitly for vcpkg installation
set(ASIO_INCLUDE_DIR "C:/Users/sarth/vcpkg/packages/asio_x64-windows/include")
message(STATUS "ASIO include directory: ${ASIO_INCLUDE_DIR}")

# Gather all .cpp files recursively in src/
file(GLOB_RECURSE SRC_FILES src/*.cpp)

# Debugging: print the list of source files
message(STATUS "SRC_FILES: ${SRC_FILES}")

# Define the resource file path
set(RESOURCE_FILE "C:/proj/Mousedroid/server/resource.rc")

# Optional: Print debug info
message(STATUS "Checking for resource file at: ${RESOURCE_FILE}")
if(EXISTS "${RESOURCE_FILE}")
    message(STATUS "Resource file found")
else()
    message(WARNING "Resource file NOT found at ${RESOURCE_FILE}")
endif()

# Handle Windows-specific files and setup
if(WIN32)
    # Add the resource file with its absolute path
    list(APPEND SRC_FILES "${RESOURCE_FILE}")
    
    # Proper way to set Windows subsystem for MSVC
    if(MSVC)
        set(CMAKE_EXE_LINKER_FLAGS "${CMAKE_EXE_LINKER_FLAGS} /SUBSYSTEM:WINDOWS")
    else()
        # For MinGW
        set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -Wl,-subsystem,windows")
    endif()

    # Add additional Windows source files
    list(APPEND SRC_FILES src/input/WindowsInputManager.cpp)

    # Set Windows-specific libraries
    set(LIBS ws2_32 wsock32)
else()
    # Handle Linux-specific files
    list(APPEND SRC_FILES src/input/LinuxInputManager.cpp)
endif()

# Check if SRC_FILES is empty and display a warning
if(NOT SRC_FILES)
    message(WARNING "No source files found!")
endif()

# Create the executable
add_executable(Mousedroid ${SRC_FILES})

# Global include directories for all targets
include_directories(
    ./include
    ${ASIO_INCLUDE_DIR}
)

# If wxWidgets is found, include it
if(wxWidgets_FOUND)
    include(${wxWidgets_USE_FILE})
    target_link_libraries(Mousedroid PRIVATE ${wxWidgets_LIBRARIES})
endif()

# Link additional libraries like Windows-specific libraries
if(DEFINED LIBS)
    target_link_libraries(Mousedroid PRIVATE ${LIBS})
endif()

# Include directories specific to the Mousedroid target
target_include_directories(Mousedroid PRIVATE 
    ./include
    ${ASIO_INCLUDE_DIR}
)

# Note: ASIO is header-only, so no need to link against it