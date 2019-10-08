if(${CMAKE_CXX_COMPILER_ID} STREQUAL MSVC)
        # boost links via preprocessor directives, so we need to set the dir in which the libs are located.
        link_directories(${USD_LIB_DIR})
endif()

add_executable (latticeMeshBoundary
        main.cpp
        )

set(Python_ADDITIONAL_VERSIONS 2.7)
find_package(PythonLibs)

target_include_directories(latticeMeshBoundary
        PUBLIC
            ${USD_INC_DIR}
            ${PYTHON_INCLUDE_PATH}
            ${USD_BOOST_INC_DIR}
       )

 set (LINK_LIBS
                ${USD_LIB_DIR}/${USD_LIB_PREFIX}gf${USD_LIB_SUFFIX}
                ${USD_LIB_DIR}/${USD_LIB_PREFIX}sdf${USD_LIB_SUFFIX}
                ${USD_LIB_DIR}/${USD_LIB_PREFIX}tf${USD_LIB_SUFFIX}
                ${USD_LIB_DIR}/${USD_LIB_PREFIX}usd${USD_LIB_SUFFIX}
                ${USD_LIB_DIR}/${USD_LIB_PREFIX}usdGeom${USD_LIB_SUFFIX}
                ${USD_LIB_DIR}/${USD_LIB_PREFIX}vt${USD_LIB_SUFFIX}
                ${PYTHON_LIBRARY}
			)

target_link_libraries(latticeMeshBoundary ${LINK_LIBS})

