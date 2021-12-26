cmake_minimum_required(VERSION 3.18)
project(game_project CXX C)

find_package(SDL2 REQUIRED)
message(STATUS "SDL2_LIBRARIES[${SDL2_LIBRARIES}] "
    "SDL2_INCLUDE_DIRS[${SDL2_INCLUDE_DIRS}]")

add_library(glad SHARED
            KHR/khrplatform.h
            glad/glad.h
            glad/glad.c)
target_compile_features(glad PUBLIC cxx_std_17)

add_library(lodepng SHARED
                    lodepng.cpp
                    lodepng.h)
target_compile_features(lodepng PUBLIC cxx_std_17)

add_executable(game_heli

                            engine.hxx
                            game.cxx

                            )
target_link_libraries(game_heli PRIVATE ${SDL2_LIBRARIES})
target_include_directories(game_heli PRIVATE ${SDL2_INCLUDE_DIRS})
target_link_libraries(game_heli PRIVATE SDL2::SDL2 SDL2::SDL2main)
target_link_libraries(game_heli PRIVATE glad)
target_link_libraries(game_heli PRIVATE lodepng)


target_compile_features(game_heli PUBLIC cxx_std_17)
