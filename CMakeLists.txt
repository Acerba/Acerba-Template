cmake_minimum_required(VERSION 2.8)

project(APP)

set(ACERBA_URL "https://github.com/Acerba/Acerba.git" CACHE STRING "Acerba Git")
set(APP_NAME "AcerbaProject" CACHE STRING "Name of application") 
set(APP_VERSION_NUM "1.0.0" CACHE STRING "Version") 
set(APP_AUTO_RESET FALSE CACHE BOOL "Reset Acerba") 


if(NOT EXISTS ${CMAKE_CURRENT_SOURCE_DIR}/acerba)
    execute_process(COMMAND git submodule add ${ACERBA_URL} acerba WORKING_DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR})
    execute_process(COMMAND git submodule update --init -- acerba WORKING_DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR})
else()

  if(APP_AUTO_RESET)
    execute_process(COMMAND git submodule foreach git checkout . WORKING_DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR})
  endif()
    execute_process(COMMAND git submodule foreach git pull -f origin master WORKING_DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR})
endif()

add_subdirectory(acerba)

file(GLOB SOURCES ${APP_SOURCE_DIR}/src/* ${APP_SOURCE_DIR}/include/*)
set(INCLUDES ${APP_SOURCE_DIR}/include ${APP_SOURCE_DIR}/acerba/include)
set(LIBS acerba)

separate_arguments(APP_NAME)
BuildApplication(${APP_NAME})

add_custom_command(TARGET ${APP_NAME} POST_BUILD
  COMMAND ${CMAKE_COMMAND} -E remove_directory 
  $<TARGET_FILE_DIR:${APP_NAME}>/assets
  COMMAND ${CMAKE_COMMAND} -E copy_directory
  ${CMAKE_SOURCE_DIR}/assets $<TARGET_FILE_DIR:${APP_NAME}>/assets
)