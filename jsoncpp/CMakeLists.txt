#dump_variables()

# bump version here
set(JSONCPP_WITH_TESTS              OFF)
set(JSONCPP_WITH_POST_BUILD_UNITTEST OFF)
set(JSONCPP_WITH_WARNING_AS_ERROR  OFF)
set(JSONCPP_WITH_STRICT_ISO        ON)
set(JSONCPP_WITH_PKGCONFIG_SUPPORT OFF)
set(JSONCPP_WITH_CMAKE_PACKAGE     OFF)
set(JSONCPP_WITH_EXAMPLE           OFF)
set(JSONCPP_STATIC_WINDOWS_RUNTIME OFF)
set(BUILD_SHARED_LIBS              OFF)
set(BUILD_STATIC_LIBS              ON)
set(BUILD_OBJECT_LIBS              OFF)
set(STATIC_SUFFIX "_real_static")
add_subdirectory(real_jsoncpp)

set(jsoncpp_VERSION 2.5)


define_module(LIBRARY jsoncpp=${jsoncpp_VERSION}
  DEPENDS BuildSystem>=1.15
  utility>=1.41
  #JSONCPP
  jsoncpp_static
  Boost
  # NB: this module provides target with different name
  PROVIDES jsoncpp-ext
  )

set(jsoncpp_SOURCES
  as.hpp
  json.hpp
  io.hpp io.cpp
)

add_library(jsoncpp-ext STATIC ${jsoncpp_SOURCES})
target_link_libraries(jsoncpp-ext ${MODULE_LIBRARIES})
target_compile_definitions(jsoncpp-ext PRIVATE ${MODULE_DEFINITIONS})

set_target_properties(jsoncpp-ext PROPERTIES LINKER_LANGUAGE CXX)
buildsys_library(jsoncpp-ext)
