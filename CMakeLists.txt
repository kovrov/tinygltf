cmake_minimum_required (VERSION 3.8)

project (tinygltf)

add_library (${PROJECT_NAME} STATIC tiny_gltf.cpp tiny_gltf.h)

set_target_properties (tinygltf PROPERTIES
  INTERFACE_INCLUDE_DIRECTORIES ${CMAKE_CURRENT_SOURCE_DIR}
)

option (ENABLE_ASAN "Compile with Address Sanitizer" OFF)
if (ENABLE_ASAN)
  set (CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -O0 -g \
    -fsanitize=address \
    -fsanitize=undefined \
    -fsanitize-address-use-after-scope \
    -fno-omit-frame-pointer"
  )
  if (NOT APPLE)
    set (CMAKE_EXE_LINKER_FLAGS ${CMAKE_EXE_LINKER_FLAGS} -fuse-ld=gold)
  endif ()
endif ()
