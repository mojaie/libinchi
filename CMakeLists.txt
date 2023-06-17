
cmake_minimum_required(VERSION 3.2)
project(inchi)

file(GLOB basesrc "INCHI_BASE/src/*.c")
file(GLOB apisrc "INCHI_API/libinchi/src/*.c")
file(GLOB ixasrc "INCHI_API/libinchi/src/ixa/*.c")
add_library(inchi SHARED ${basesrc} ${apisrc} ${ixasrc})

target_compile_definitions(inchi PUBLIC TARGET_API_LIB)
target_compile_definitions(inchi PUBLIC COMPILE_ANSI_ONLY)
set_target_properties(inchi
  PROPERTIES
    VERSION 1.06
    SOVERSION 1
)

install(
  TARGETS inchi
  EXPORT inchi-targets
  ARCHIVE DESTINATION lib
  LIBRARY DESTINATION lib
)
    
file(GLOB basehdr "INCHI_BASE/src/*.h")
file(GLOB apihdr "INCHI_API/libinchi/src/*.h")
file(GLOB ixahdr "INCHI_API/libinchi/src/ixa/*.h")
install(FILES ${basehdr} ${apihdr} ${ixahdr} DESTINATION include)

install(
  EXPORT inchi-targets
  FILE ${PROJECT_NAME}-config.cmake
  DESTINATION lib/cmake
)
