cmake_minimum_required (VERSION 3.0)
project (SUPERLU VERSION 4.3 LANGUAGES C Fortran)

option(BUILD_TESTS "${PROJECT_NAME} - Build tests" ON)
set(PACKAGE_CONFIG_DIR "lib/cmake" CACHE STRING "Directory for package config files (relative to CMAKE_INSTALL_PREFIX)")
set(BUILD_PRECISION sdcz CACHE STRING "${PROJECT_NAME} - Build precisions (sdcz)")
if (BUILD_SHARED_LIBS)
    # This will cause all the OBJECT targets to have -fPIC as well.
    SET(CMAKE_POSITION_INDEPENDENT_CODE ON)
endif()

find_package(BLAS ${BLAS_VERSION} REQUIRED)
if (BUILD_TESTS)
    find_package(LAPACK ${LAPACK_VERSION} REQUIRED)
endif()

add_subdirectory(SRC)

if (BUILD_TESTS)
    enable_testing()
    add_subdirectory(TESTING)
    add_subdirectory(EXAMPLE)
    add_subdirectory(FORTRAN)
endif()
