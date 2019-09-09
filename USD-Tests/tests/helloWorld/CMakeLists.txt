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

set (LINK_LIBS
        ${USD_LIB_DIR}/${USD_LIB_PREFIX}hd${USD_LIB_SUFFIX}
        ${USD_LIB_DIR}/${USD_LIB_PREFIX}hdSt${USD_LIB_SUFFIX}
        ${USD_LIB_DIR}/${USD_LIB_PREFIX}hdx${USD_LIB_SUFFIX}
        ${USD_LIB_DIR}/${USD_LIB_PREFIX}tf${USD_LIB_SUFFIX}
        ${USD_LIB_DIR}/${USD_LIB_PREFIX}usd${USD_LIB_SUFFIX}
        ${USD_LIB_DIR}/${USD_LIB_PREFIX}usdGeom${USD_LIB_SUFFIX}
        ${USD_LIB_DIR}/${USD_LIB_PREFIX}sdf${USD_LIB_SUFFIX}
        ${USD_LIB_DIR}/${USD_LIB_PREFIX}garch${USD_LIB_SUFFIX}
        ${USD_LIB_DIR}/${USD_LIB_PREFIX}cameraUtil${USD_LIB_SUFFIX}
        ${USD_LIB_DIR}/${USD_LIB_PREFIX}gf${USD_LIB_SUFFIX}
        ${USD_LIB_DIR}/${USD_LIB_PREFIX}glf${USD_LIB_SUFFIX}
        ${USD_LIB_DIR}/${USD_LIB_PREFIX}vt${USD_LIB_SUFFIX}
        ${USD_LIB_DIR}/${USD_LIB_PREFIX}pxOsd${USD_LIB_SUFFIX}
        ${USD_LIB_DIR}/${USD_LIB_PREFIX}osdCPU${USD_LIB_SUFFIX}
        ${PYTHON_LIBRARY}
        ${OPENGL_LIBRARIES}
)
if(NOT ${CMAKE_SYSTEM_NAME} MATCHES "Windows")
        message(STATUS "Not Windows!")
        # this library is not needed on windows builds (linked via pragmas aready by boost)
        list(APPEND LINK_LIBS ${USD_LIB_DIR}/${USD_LIB_PREFIX}boost_python${USD_LIB_SUFFIX}) # todo find library (but appears to not be necessary)
endif()
message (STATUS ${LINK_LIBS})

target_link_libraries( helloWorld ${LINK_LIBS} )
