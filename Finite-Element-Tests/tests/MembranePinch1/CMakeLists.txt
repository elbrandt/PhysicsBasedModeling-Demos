set(TARGET_NAME MembranePinch1)

if(${CMAKE_CXX_COMPILER_ID} STREQUAL MSVC)
        # boost links via preprocessor directives, so we need to set the dir in which the libs are located.
        link_directories(${USD_LIB_DIR})
endif()

add_executable (${TARGET_NAME}
        main.cpp
        )

target_include_directories(${TARGET_NAME}
        PUBLIC
            ${USD_INC_DIR}
            ${EIGEN3_INCLUDE_DIR}
            ${USD_BOOST_INC_DIR}
            ${PYTHON_INCLUDE_PATH}
        )

target_link_libraries(
		${TARGET_NAME}
                ${USD_LIB_DIR}/${USD_LIB_PREFIX}gf${USD_LIB_SUFFIX}
                ${USD_LIB_DIR}/${USD_LIB_PREFIX}sdf${USD_LIB_SUFFIX}
                ${USD_LIB_DIR}/${USD_LIB_PREFIX}tf${USD_LIB_SUFFIX}
                ${USD_LIB_DIR}/${USD_LIB_PREFIX}usd${USD_LIB_SUFFIX}
                ${USD_LIB_DIR}/${USD_LIB_PREFIX}usdGeom${USD_LIB_SUFFIX}
                ${USD_LIB_DIR}/${USD_LIB_PREFIX}vt${USD_LIB_SUFFIX}
                ${PYTHON_LIBRARY}
        )