cmake_minimum_required(VERSION 3.16)

project(lua-proj)

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

target_include_directories(lua PUBLIC ${CMAKE_CURRENT_SOURCE_DIR}/include)
target_include_directories(lua PRIVATE ${CMAKE_CURRENT_SOURCE_DIR}/include/lua)
