cmake_minimum_required(VERSION 3.25)
project(roboticstoolbox LANGUAGES CXX C)

# Python + NumPy
find_package(Python COMPONENTS Interpreter Development.Module NumPy REQUIRED)

Python_add_library(frne MODULE
    roboticstoolbox/core/vmath.c
    roboticstoolbox/core/ne.c
    roboticstoolbox/core/frne.c
    WITH_SOABI)
target_compile_features(frne PRIVATE c_std_17)
target_include_directories(frne PRIVATE
    ${Python_NumPy_INCLUDE_DIRS}
    ${CMAKE_CURRENT_SOURCE_DIR}/roboticstoolbox/core
)
target_link_libraries(frne PRIVATE Python::Module)

install(TARGETS frne LIBRARY DESTINATION roboticstoolbox)

Python_add_library(fknm MODULE
    roboticstoolbox/core/methods.cpp
    roboticstoolbox/core/ik.cpp
    roboticstoolbox/core/linalg.cpp
    roboticstoolbox/core/fknm.cpp
    WITH_SOABI)
target_compile_features(fknm PRIVATE cxx_std_17)
target_include_directories(fknm PRIVATE
    ${Python_NumPy_INCLUDE_DIRS}
    ${CMAKE_CURRENT_SOURCE_DIR}/roboticstoolbox/core
)
target_link_libraries(fknm PRIVATE Python::Module Python::NumPy)


install(TARGETS fknm LIBRARY DESTINATION roboticstoolbox)
