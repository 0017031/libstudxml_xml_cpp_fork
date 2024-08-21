cmake_minimum_required(VERSION 3.20)

if(CMAKE_CURRENT_SOURCE_DIR STREQUAL CMAKE_SOURCE_DIR) # stand-alone
  message("project(libstudxml)")
  project(libstudxml)
else() # reffered by add_subdirectory()
  message("lib: libstudxml\t(${CMAKE_BUILD_TYPE})")
endif()
set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

add_subdirectory(examples)
add_subdirectory(tests)


set(LIBSTUDXML_ROOT_DIR ${CMAKE_CURRENT_SOURCE_DIR})
set(LIBSTUDXML_INCLUDE_DIR ${LIBSTUDXML_ROOT_DIR})
set(EXPAT_INCLUDE_DIRS ${LIBSTUDXML_ROOT_DIR}/libstudxml/details/expat)

set(LIBSTUDXML
  ${LIBSTUDXML_ROOT_DIR}/libstudxml/parser.cxx
  ${LIBSTUDXML_ROOT_DIR}/libstudxml/qname.cxx
  ${LIBSTUDXML_ROOT_DIR}/libstudxml/serializer.cxx
  ${LIBSTUDXML_ROOT_DIR}/libstudxml/value-traits.cxx

  ${LIBSTUDXML_ROOT_DIR}/libstudxml/content.hxx
  ${LIBSTUDXML_ROOT_DIR}/libstudxml/exception.hxx
  ${LIBSTUDXML_ROOT_DIR}/libstudxml/forward.hxx
)

set(GENX
  ${LIBSTUDXML_ROOT_DIR}/libstudxml/details/genx/char-props.c
  ${LIBSTUDXML_ROOT_DIR}/libstudxml/details/genx/genx.c

  ${LIBSTUDXML_ROOT_DIR}/libstudxml/details/genx/genx.h
)

set(EXPAT
  ${LIBSTUDXML_ROOT_DIR}/libstudxml/details/expat/xmlparse.c
  ${LIBSTUDXML_ROOT_DIR}/libstudxml/details/expat/xmlrole.c
  ${LIBSTUDXML_ROOT_DIR}/libstudxml/details/expat/xmltok.c
  ${LIBSTUDXML_ROOT_DIR}/libstudxml/details/expat/xmltok_impl.c
  ${LIBSTUDXML_ROOT_DIR}/libstudxml/details/expat/xmltok_ns.c

  ${LIBSTUDXML_ROOT_DIR}/libstudxml/details/expat/ascii.h
  ${LIBSTUDXML_ROOT_DIR}/libstudxml/details/expat/asciitab.h
  ${LIBSTUDXML_ROOT_DIR}/libstudxml/details/expat/config.h
  ${LIBSTUDXML_ROOT_DIR}/libstudxml/details/expat/expat_external.h
  ${LIBSTUDXML_ROOT_DIR}/libstudxml/details/expat/expat.h
  ${LIBSTUDXML_ROOT_DIR}/libstudxml/details/expat/iasciitab.h
  ${LIBSTUDXML_ROOT_DIR}/libstudxml/details/expat/internal.h
  ${LIBSTUDXML_ROOT_DIR}/libstudxml/details/expat/latin1tab.h
  ${LIBSTUDXML_ROOT_DIR}/libstudxml/details/expat/nametab.h
  ${LIBSTUDXML_ROOT_DIR}/libstudxml/details/expat/utf8tab.h
  ${LIBSTUDXML_ROOT_DIR}/libstudxml/details/expat/xmlrole.h
  ${LIBSTUDXML_ROOT_DIR}/libstudxml/details/expat/xmltok_impl.h
  ${LIBSTUDXML_ROOT_DIR}/libstudxml/details/expat/xmltok.h
)

add_library(libstudxml OBJECT ${LIBSTUDXML} ${GENX} ${EXPAT})

target_include_directories(libstudxml
  PUBLIC ${LIBSTUDXML_ROOT_DIR}
  PUBLIC ${EXPAT_INCLUDE_DIRS}
)
