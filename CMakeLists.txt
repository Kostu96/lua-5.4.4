cmake_minimum_required(VERSION 3.16...3.24)

project(lua-proj VERSION 5.4.4)

set(LUA_MAIN_PROJECT OFF)
if(CMAKE_SOURCE_DIR STREQUAL PROJECT_SOURCE_DIR)
  set(LUA_MAIN_PROJECT ON)
endif()
set(CMAKE_DEBUG_POSTFIX "d")

option(LUA_INSTALL "Generate install target" ${LUA_MAIN_PROJECT})

set(LUA_HEADERS
    ${CMAKE_CURRENT_SOURCE_DIR}/include/lua/lualib.h
    ${CMAKE_CURRENT_SOURCE_DIR}/include/lua/lauxlib.h
    ${CMAKE_CURRENT_SOURCE_DIR}/include/lua/lua.h
    ${CMAKE_CURRENT_SOURCE_DIR}/include/lua/lua.hpp
    ${CMAKE_CURRENT_SOURCE_DIR}/include/lua/luaconf.h
)

set(LUA_SOURCES
    ${CMAKE_CURRENT_SOURCE_DIR}/src/lapi.c
    ${CMAKE_CURRENT_SOURCE_DIR}/src/lapi.h
    ${CMAKE_CURRENT_SOURCE_DIR}/src/lauxlib.c
    ${CMAKE_CURRENT_SOURCE_DIR}/src/lbaselib.c
    ${CMAKE_CURRENT_SOURCE_DIR}/src/lcode.c
    ${CMAKE_CURRENT_SOURCE_DIR}/src/lcode.h
    ${CMAKE_CURRENT_SOURCE_DIR}/src/lcorolib.c
    ${CMAKE_CURRENT_SOURCE_DIR}/src/lctype.c
    ${CMAKE_CURRENT_SOURCE_DIR}/src/lctype.h
    ${CMAKE_CURRENT_SOURCE_DIR}/src/ldblib.c
    ${CMAKE_CURRENT_SOURCE_DIR}/src/ldebug.c
    ${CMAKE_CURRENT_SOURCE_DIR}/src/ldebug.h
    ${CMAKE_CURRENT_SOURCE_DIR}/src/ldo.c
    ${CMAKE_CURRENT_SOURCE_DIR}/src/ldo.h
    ${CMAKE_CURRENT_SOURCE_DIR}/src/ldump.c
    ${CMAKE_CURRENT_SOURCE_DIR}/src/lfunc.c
    ${CMAKE_CURRENT_SOURCE_DIR}/src/lfunc.h
    ${CMAKE_CURRENT_SOURCE_DIR}/src/lgc.c
    ${CMAKE_CURRENT_SOURCE_DIR}/src/lgc.h
    ${CMAKE_CURRENT_SOURCE_DIR}/src/linit.c
    ${CMAKE_CURRENT_SOURCE_DIR}/src/liolib.c
    ${CMAKE_CURRENT_SOURCE_DIR}/src/ljumptab.h
    ${CMAKE_CURRENT_SOURCE_DIR}/src/llex.c
    ${CMAKE_CURRENT_SOURCE_DIR}/src/llex.h
    ${CMAKE_CURRENT_SOURCE_DIR}/src/llimits.h
    ${CMAKE_CURRENT_SOURCE_DIR}/src/lmathlib.c
    ${CMAKE_CURRENT_SOURCE_DIR}/src/lmem.c
    ${CMAKE_CURRENT_SOURCE_DIR}/src/lmem.h
    ${CMAKE_CURRENT_SOURCE_DIR}/src/loadlib.c
    ${CMAKE_CURRENT_SOURCE_DIR}/src/lobject.c
    ${CMAKE_CURRENT_SOURCE_DIR}/src/lobject.h
    ${CMAKE_CURRENT_SOURCE_DIR}/src/lopcodes.c
    ${CMAKE_CURRENT_SOURCE_DIR}/src/lopcodes.h
    ${CMAKE_CURRENT_SOURCE_DIR}/src/lopnames.h
    ${CMAKE_CURRENT_SOURCE_DIR}/src/loslib.c
    ${CMAKE_CURRENT_SOURCE_DIR}/src/lparser.c
    ${CMAKE_CURRENT_SOURCE_DIR}/src/lparser.h
    ${CMAKE_CURRENT_SOURCE_DIR}/src/lprefix.h
    ${CMAKE_CURRENT_SOURCE_DIR}/src/lstate.c
    ${CMAKE_CURRENT_SOURCE_DIR}/src/lstate.h
    ${CMAKE_CURRENT_SOURCE_DIR}/src/lstring.c
    ${CMAKE_CURRENT_SOURCE_DIR}/src/lstring.h
    ${CMAKE_CURRENT_SOURCE_DIR}/src/lstrlib.c
    ${CMAKE_CURRENT_SOURCE_DIR}/src/ltable.c
    ${CMAKE_CURRENT_SOURCE_DIR}/src/ltable.h
    ${CMAKE_CURRENT_SOURCE_DIR}/src/ltablib.c
    ${CMAKE_CURRENT_SOURCE_DIR}/src/ltm.c
    ${CMAKE_CURRENT_SOURCE_DIR}/src/ltm.h
    #${CMAKE_CURRENT_SOURCE_DIR}/src/lua.c
    #${CMAKE_CURRENT_SOURCE_DIR}/src/luac.c
    ${CMAKE_CURRENT_SOURCE_DIR}/src/lundump.c
    ${CMAKE_CURRENT_SOURCE_DIR}/src/lundump.h
    ${CMAKE_CURRENT_SOURCE_DIR}/src/lutf8lib.c
    ${CMAKE_CURRENT_SOURCE_DIR}/src/lvm.c
    ${CMAKE_CURRENT_SOURCE_DIR}/src/lvm.h
    ${CMAKE_CURRENT_SOURCE_DIR}/src/lzio.c
    ${CMAKE_CURRENT_SOURCE_DIR}/src/lzio.h
)

add_library(lua STATIC
    ${LUA_HEADERS}
    ${LUA_SOURCES}
)

source_group(TREE ${CMAKE_CURRENT_SOURCE_DIR}/include/lua PREFIX source FILES ${LUA_HEADERS})
source_group(TREE ${CMAKE_CURRENT_SOURCE_DIR}/src PREFIX source FILES ${LUA_SOURCES})

target_include_directories(lua INTERFACE
    $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/include>
    $<INSTALL_INTERFACE:include>)

target_include_directories(lua PRIVATE ${CMAKE_CURRENT_SOURCE_DIR}/include/lua)

set_target_properties(lua PROPERTIES
    DEBUG_POSTFIX "${CMAKE_DEBUG_POSTFIX}")

add_library(lua::lua ALIAS lua)

if (${LUA_INSTALL})
    include(GNUInstallDirs)
    
    install(TARGETS lua
        EXPORT luaTargets
        INCLUDES DESTINATION include)
    
    install(DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR}/include/lua DESTINATION include)
    
    install(EXPORT luaTargets
        NAMESPACE lua::
        FILE luaTargets.cmake
        DESTINATION lib/cmake/lua)
        
    include(CMakePackageConfigHelpers)
    
    configure_package_config_file(${CMAKE_CURRENT_SOURCE_DIR}/luaConfig.cmake.in "${CMAKE_CURRENT_BINARY_DIR}/luaConfig.cmake"
        INSTALL_DESTINATION "lib/cmake/lua"
        NO_SET_AND_CHECK_MACRO
        NO_CHECK_REQUIRED_COMPONENTS_MACRO)
        
    write_basic_package_version_file("${CMAKE_CURRENT_BINARY_DIR}/luaConfigVersion.cmake"
        VERSION ${PROJECT_VERSION}
        COMPATIBILITY AnyNewerVersion)
        
    install(FILES
        ${CMAKE_CURRENT_BINARY_DIR}/luaConfig.cmake
        ${CMAKE_CURRENT_BINARY_DIR}/luaConfigVersion.cmake
        DESTINATION lib/cmake/lua)
        
    export(EXPORT luaTargets
        NAMESPACE lua::
        FILE "${CMAKE_CURRENT_BINARY_DIR}/luaTargets.cmake")
endif()
