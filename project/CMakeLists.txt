add_executable("${PROJECT_NAME}" "Main.cpp")


add_subdirectory("include")
add_subdirectory("src")


# Add includes to target
target_include_directories("${PROJECT_NAME}" PUBLIC
$<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/include>
$<BUILD_INTERFACE:${CMAKE_CURRENT_BINARY_DIR}>
$<INSTALL_INTERFACE:include>
)

