cmake_minimum_required(VERSION 3.2)

project(FEM-Explicit-2D)
enable_language(Fortran )
        

if(CMAKE_Fortran_COMPILER_ID MATCHES Intel)
    set(CMAKE_Fortran_FLAGS         "${CMAKE_Fortran_FLAGS} -Wall"})
    set(CMAKE_Fortran_FLAGS_DEBUG   "-g -traceback")
    set(CMAKE_Fortran_FLAGS_RELEASE "-O3 -ip -xHOST")
endif()

if(CMAKE_Fortran_COMPILER_ID MATCHES GNU)
    set(CMAKE_Fortran_FLAGS         "${CMAKE_Fortran_FLAGS} -Wall")
    set(CMAKE_Fortran_FLAGS_DEBUG   "-O0 -g3")
    set(CMAKE_Fortran_FLAGS_RELEASE "-Ofast -march=native")
endif()

file(GLOB_RECURSE sources *.f90)

add_executable(FEM-Explicit-2D ${sources} ) #Single case 1 element        

LINK_DIRECTORIES(${LAPACK_BIN_DIR} ${BLAS_BIN_DIR})
# if (NOT WIN32)
 TARGET_LINK_LIBRARIES(FEM-Explicit-2D lapack blas )
 # else ()
  # TARGET_LINK_LIBRARIES(FEM-Explicit-2D lapack cblas )
# endif()

