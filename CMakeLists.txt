#Dependencies.
if( NOT TARGET PkgConfig::TREESITTER )
	message(
		FATAL_ERROR
		"Expected a CMake target named 'PkgConfig::TREESITTER'. Add it via add_subdirectory() or find_package() before including this directory."
	)
endif()



add_library( cpp-tree-sitter INTERFACE )

target_include_directories(
	cpp-tree-sitter
	INTERFACE
		$<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/include>
		$<INSTALL_INTERFACE:include>
)

target_link_libraries(
	cpp-tree-sitter
	INTERFACE
		PkgConfig::TREESITTER
		${TREESITTER_CPP_LIBRARY}
)
