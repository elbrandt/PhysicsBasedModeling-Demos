cmake_minimum_required (VERSION 2.8.11)
set (CMAKE_CXX_STANDARD 11)

project (Simple-Deformations CXX)

if(${CMAKE_CXX_COMPILER_ID} STREQUAL MSVC)
    # windows.h defines max as a macro, which interferes with std::limits<>::max()
    add_compile_definitions(NOMINMAX)
    # disable warnings about some casting inconsistencies
    set (CMAKE_CXX_FLAGS "/wd\"4244\" /wd\"4305\" /wd\"4267\" ${CMAKE_CXX_FLAGS}")
    # lib suffix is different on windows than ubuntu
    # surely cmake can take care of this automatically, but I don't know how.
    set (USD_LIB_PREFIX ${CMAKE_STATIC_LIBRARY_PREFIX}) # linking on with MSVC is different
    set (USD_LIB_SUFFIX ${CMAKE_STATIC_LIBRARY_SUFFIX})
else() # Assuming UNIX
	message(STATUS "Ubuntu!")
    set (CMAKE_CXX_FLAGS "-Wno-deprecated ${CMAKE_CXX_FLAGS}")
    set (USD_LIB_PREFIX ${CMAKE_SHARED_LIBRARY_PREFIX})
    set (USD_LIB_SUFFIX ${CMAKE_SHARED_LIBRARY_SUFFIX})
endif()

add_definitions(-DBUILD_COMPONENT_SRC_PREFIX="" -DBUILD_OPTLEVEL_DEV)

if(${CMAKE_CXX_COMPILER_ID} STREQUAL MSVC)
  set(USD_ROOT_DIR "D:/buildtools/usd_dbg")
else() # UNIX
  set(USD_ROOT_DIR "/usr/local/USD")
endif()

set(USD_LIB_DIR ${USD_ROOT_DIR}/lib/)
set(USD_INC_DIR ${USD_ROOT_DIR}/include/)
if(${CMAKE_CXX_COMPILER_ID} STREQUAL MSVC)
    set(USD_BOOST_INC_DIR ${USD_INC_DIR}/boost-1_65_1)
endif()

set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/bin)

add_subdirectory(tests)
