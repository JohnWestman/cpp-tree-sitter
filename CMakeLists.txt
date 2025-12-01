#Dependencies.
if( NOT TARGET PkgConfig::TREESITTER )
	message(
		FATAL_ERROR
		"Expected a CMake target named 'PkgConfig::TREESITTER'. Add it via add_subdirectory() or find_package() before including this directory."
	)
endif()




set( CMAKE_CXX_STANDARD			 23 )
set( CMAKE_CXX_STANDARD_REQUIRED ON )

add_library( cpp-tree-sitter INTERFACE )
set(
	FlagsDebug
	-pipe
	-O0
	-ggdb3
	-Wall
	-fno-inline
	-fno-unroll-loops
	-fno-reorder-blocks
)


#add_compile_options(
#	-fPIC
#	${FlagsDebug}
#)

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
