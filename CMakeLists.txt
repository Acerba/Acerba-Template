cmake_minimum_required(VERSION 2.8)

project(APP)

set(ACERBA_URL "https://github.com/Acerba/Acerba.git" CACHE STRING "Acerba Git")
set(APP_NAME "AcerbaProject" CACHE STRING "Name of application") 
set(APP_VERSION_NUM "1.0.0" CACHE STRING "Version") 


if(NOT EXISTS ${CMAKE_CURRENT_SOURCE_DIR}/acerba)
    execute_process(COMMAND git submodule add ${ACERBA_URL} acerba WORKING_DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR})
    execute_process(COMMAND git submodule update --init -- acerba WORKING_DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR})
else()
    execute_process(COMMAND git submodule update --merge -- acerba WORKING_DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR})
endif()

add_subdirectory(acerba)

file(GLOB SOURCES ${APP_SOURCE_DIR}/src/* ${APP_SOURCE_DIR}/include/*)
set(INCLUDES ${APP_SOURCE_DIR}/include ${APP_SOURCE_DIR}/acerba/include)
set(LIBS acerba)

separate_arguments(APP_NAME)
BuildApplication(${APP_NAME})

