if(${CMAKE_SYSTEM_NAME} MATCHES "Windows") # we'll assume 'Windows' means MSVC for simplicity
        # boost links via preprocessor directives, so we need to set the dir in which the libs are located.
        link_directories(${USD_LIB_DIR})
endif()

add_executable (animateAttribute
        main.cpp
        )

find_package(PythonLibs)

target_include_directories(animateAttribute
        PUBLIC
            ${USD_INC_DIR}
            ${PYTHON_INCLUDE_PATH}
            ${USD_BOOST_INC_DIR}
        )

target_link_libraries(
        animateAttribute
                ${USD_LIB_DIR}/${CMAKE_STATIC_LIBRARY_PREFIX}gf${CMAKE_STATIC_LIBRARY_SUFFIX}
                ${USD_LIB_DIR}/${CMAKE_STATIC_LIBRARY_PREFIX}sdf${CMAKE_STATIC_LIBRARY_SUFFIX}
                ${USD_LIB_DIR}/${CMAKE_STATIC_LIBRARY_PREFIX}tf${CMAKE_STATIC_LIBRARY_SUFFIX}
                ${USD_LIB_DIR}/${CMAKE_STATIC_LIBRARY_PREFIX}usd${CMAKE_STATIC_LIBRARY_SUFFIX}
                ${USD_LIB_DIR}/${CMAKE_STATIC_LIBRARY_PREFIX}usdGeom${CMAKE_STATIC_LIBRARY_SUFFIX}
                ${USD_LIB_DIR}/${CMAKE_STATIC_LIBRARY_PREFIX}vt${CMAKE_STATIC_LIBRARY_SUFFIX}
                # ${USD_LIB_DIR}/${CMAKE_STATIC_LIBRARY_PREFIX}boost_python.so # todo find library
                ${PYTHON_LIBRARY}
        )
