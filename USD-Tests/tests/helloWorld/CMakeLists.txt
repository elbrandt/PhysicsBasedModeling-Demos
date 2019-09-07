
if(${CMAKE_SYSTEM_NAME} MATCHES "Windows") # we'll assume 'Windows' means MSVC for simplicity
        # boost links via preprocessor directives, so we need to set the dir in which the libs are located.
        link_directories(${USD_LIB_DIR})
endif()

add_executable (helloWorld
        main.cpp
        )

find_package(PythonLibs)
find_package(OpenGL)

target_include_directories(helloWorld
        PUBLIC
            ${USD_INC_DIR}
            ${PYTHON_INCLUDE_PATH}
            ${USD_BOOST_INC_DIR}
        )

target_link_libraries(
        helloWorld
                ${USD_LIB_DIR}/${CMAKE_STATIC_LIBRARY_PREFIX}hd${CMAKE_STATIC_LIBRARY_SUFFIX}
                ${USD_LIB_DIR}/${CMAKE_STATIC_LIBRARY_PREFIX}hdSt${CMAKE_STATIC_LIBRARY_SUFFIX}
                ${USD_LIB_DIR}/${CMAKE_STATIC_LIBRARY_PREFIX}hdx${CMAKE_STATIC_LIBRARY_SUFFIX}
                ${USD_LIB_DIR}/${CMAKE_STATIC_LIBRARY_PREFIX}tf${CMAKE_STATIC_LIBRARY_SUFFIX}
                ${USD_LIB_DIR}/${CMAKE_STATIC_LIBRARY_PREFIX}usd${CMAKE_STATIC_LIBRARY_SUFFIX}
                ${USD_LIB_DIR}/${CMAKE_STATIC_LIBRARY_PREFIX}usdGeom${CMAKE_STATIC_LIBRARY_SUFFIX}
                ${USD_LIB_DIR}/${CMAKE_STATIC_LIBRARY_PREFIX}sdf${CMAKE_STATIC_LIBRARY_SUFFIX}
                ${USD_LIB_DIR}/${CMAKE_STATIC_LIBRARY_PREFIX}garch${CMAKE_STATIC_LIBRARY_SUFFIX}
                ${USD_LIB_DIR}/${CMAKE_STATIC_LIBRARY_PREFIX}cameraUtil${CMAKE_STATIC_LIBRARY_SUFFIX}
                ${USD_LIB_DIR}/${CMAKE_STATIC_LIBRARY_PREFIX}gf${CMAKE_STATIC_LIBRARY_SUFFIX}
                ${USD_LIB_DIR}/${CMAKE_STATIC_LIBRARY_PREFIX}glf${CMAKE_STATIC_LIBRARY_SUFFIX}
                ${USD_LIB_DIR}/${CMAKE_STATIC_LIBRARY_PREFIX}vt${CMAKE_STATIC_LIBRARY_SUFFIX}
                ${USD_LIB_DIR}/${CMAKE_STATIC_LIBRARY_PREFIX}pxOsd${CMAKE_STATIC_LIBRARY_SUFFIX}
                ${USD_LIB_DIR}/${CMAKE_STATIC_LIBRARY_PREFIX}osdCPU${CMAKE_STATIC_LIBRARY_SUFFIX}
                # ${USD_LIB_DIR}/libboost_python # todo find library (but appears to not be necessary)
                ${PYTHON_LIBRARY}
                ${OPENGL_LIBRARIES}
        )



