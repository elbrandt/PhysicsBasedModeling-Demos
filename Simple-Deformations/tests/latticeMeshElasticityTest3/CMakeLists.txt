if(${CMAKE_CXX_COMPILER_ID} STREQUAL MSVC)
        # boost links via preprocessor directives, so we need to set the dir in which the libs are located.
        link_directories(${USD_LIB_DIR})
endif()

add_executable (latticeMeshElasticityTest3
        main.cpp
        )

set(Python_ADDITIONAL_VERSIONS 2.7)
find_package(PythonLibs)
find_package(Eigen3)

target_include_directories(latticeMeshElasticityTest3
        PUBLIC
            ${USD_INC_DIR}
            ${PYTHON_INCLUDE_PATH}
            ${USD_BOOST_INC_DIR}
            ${EIGEN3_INCLUDE_DIR}
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

if (NOT ${CMAKE_CXX_COMPILER_ID} STREQUAL MSVC)
        # this library is not needed on windows builds (linked via pragmas aready by boost)
        list(APPEND LINK_LIBS ${USD_LIB_DIR}/${USD_LIB_PREFIX}boost_python${USD_LIB_SUFFIX}) # todo find library (but appears to not be necessary)
endif()

if (NOT ${CMAKE_CXX_COMPILER_ID} STREQUAL MSVC)
        # this library is not needed on windows builds (linked via pragmas aready by boost)
        list(APPEND LINK_LIBS ${USD_LIB_DIR}/${USD_LIB_PREFIX}boost_python${USD_LIB_SUFFIX}) # todo find library (but appears to not be necessary)
endif()

target_link_libraries(latticeMeshElasticityTest3 ${LINK_LIBS})

