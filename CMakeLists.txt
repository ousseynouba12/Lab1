cmake_minimum_required(VERSION 3.28)
project(labo01 CXX)

set(CMAKE_CXX_STANDARD 20)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_CXX_EXTENSIONS OFF)

# Avertissements du cours : on les lit, on les corrige.
if(MSVC)
    add_compile_options(/W4)
else()
    add_compile_options(-Wall -Wextra -Wpedantic -Wconversion)
endif()

# Un fichier source par ligne ; CLion propose de les ajouter ici.
add_executable(presentation
        main.cpp
)
