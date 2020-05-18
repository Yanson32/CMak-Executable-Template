cmake_minimum_required(VERSION "3.5.0")


project("Example")


add_subdirectory("project")


# Add cpack 
include("CPackConfig")
include("CPack")
