cmake_minimum_required (VERSION 3.4)


add_library (openvdb_boost INTERFACE)
if (NOT DEFINED     BOOST_ROOT        AND
    NOT DEFINED ENV{BOOST_ROOT}       AND
    NOT DEFINED     BOOST_INCLUDEDIR  AND
    NOT DEFINED ENV{BOOST_INCLUDEDIR} AND
    NOT DEFINED     BOOST_LIBRARYDIR  AND
    NOT DEFINED ENV{BOOST_LIBRARYDIR})
    if (APPLE)
        set(BOOST_ROOT ${CMAKE_CURRENT_SOURCE_DIR})
    elseif (WIN32)
        #set(BOOST_INCLUDEDIR "C:/local/boost_1_55_0")
        #set(BOOST_LIBRARYDIR "C:/local/boost_1_55_0/lib32-msvc-10.0")
    endif()
endif()
if (APPLE OR WIN32)
    set(Boost_USE_STATIC_LIBS TRUE)
endif()
find_package(Boost 1.32 REQUIRED COMPONENTS iostreams system thread)
include_directories(SYSTEM ${Boost_INCLUDE_DIRS})

target_link_libraries(openvdb_boost
    INTERFACE 
        ${Boost_LIBRARIES})