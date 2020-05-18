# The FILES variable contains absolute paths to all the source files in this directory.
set(FILES "${CMAKE_CURRENT_LIST_DIR}/hello.cpp")


# The DIRECTORIES variable is a list of all the subdirectories in this directory.
set(DIRECTORIES "")


# Add all subdirectories
foreach(DIR ${DIRECTORIESS})
	add_subdirectory("${DIR}")
endforeach()


# If the files variable is not empty
if(FILES)
	# Add all files to existing target
	target_sources("${PROJECT_NAME}" PRIVATE ${FILES})
endif()
