
SET(PROJECT_NAME icl_googletest)
STRING(TOUPPER ${PROJECT_NAME} PROJECT_NAME_UPPER)

# include icmaker if not already available
IF(NOT DEFINED ICMAKER_DIRECTORY)
  FIND_PACKAGE(icmaker REQUIRED)
  INCLUDE(UseFullIcMaker REQUIRED)
ENDIF()

PROJECT(${PROJECT_NAME})

FIND_PACKAGE(Threads REQUIRED)

# enable C++11 support
if (CMAKE_VERSION VERSION_LESS "3.1")
  if (CMAKE_CXX_COMPILER_ID STREQUAL "GNU")
    set (CMAKE_CXX_FLAGS "-std=gnu++11 ${CMAKE_CXX_FLAGS}")
    set (CMAKE_CXX_FLAGS "-march=native ${CMAKE_CXX_FLAGS}")
  endif ()
else ()
  set (CMAKE_CXX_STANDARD 11)
  # enable vectorization and other platform dependant optimizations
  set (CMAKE_CXX_FLAGS "-march=native ${CMAKE_CXX_FLAGS}")
endif ()

ADD_SUBDIRECTORY(ext/gtest)

ICMAKER_REGISTER_PACKAGE(${PROJECT_NAME})
ICMAKER_CONFIGURE_PACKAGE()
