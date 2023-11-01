cmake_minimum_required(VERSION 3.14)

project(flat_vector LANGUAGES CXX)

option(FLAT_VECTOR_TESTING "Включить модульное тестирование" ON)

option(ENABLE_WARNING "Включить предупреждения" OFF)

if (ENABLE_WARNING)
    if((CMAKE_CXX_COMPILER_ID MATCHES "GNU") OR (CMAKE_CXX_COMPILER_ID MATCHES "Clang"))
        add_compile_options(
            -Wall
            -Wextra
            -Wpedantic

            -Wcast-align
            -Wcast-qual
            -Wconversion
            -Wctor-dtor-privacy
            -Wenum-compare
            -Wfloat-equal
            -Wnon-virtual-dtor
            -Wold-style-cast
            -Woverloaded-virtual
            -Wredundant-decls
            -Wsign-conversion
            -Wsign-promo
        )
    elseif(CMAKE_CXX_COMPILER_ID MATCHES "MSVC")
        add_compile_options(/W4 /WX)
    endif()

    if(NOT CMAKE_CXX_EXTENSIONS)
        set(CMAKE_CXX_EXTENSIONS OFF)
    endif()
endif()   

add_library(flat_vector_header INTERFACE)
target_include_directories(flat_vector_header INTERFACE headers)
add_library(flat_vector::header ALIAS flat_vector_header)

if(NOT FLAT_VECTOR_TESTING)
    message(STATUS "Тестирование выключено")
else()
    add_subdirectory(test)
endif()

