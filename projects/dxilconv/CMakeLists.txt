set(DXILCONV_PROJECT_SOURCE_DIR ${CMAKE_CURRENT_SOURCE_DIR})
set(DXILCONV_PROJECT_BINARY_DIR ${CMAKE_CURRENT_BINARY_DIR})

include_directories(
  ${LLVM_MAIN_INCLUDE_DIR}
  ${DXC_PROJECTS_SOURCE_DIR}/include
  ${DXC_PROJECTS_BINARY_DIR}/include
  ${DXILCONV_PROJECT_SOURCE_DIR}/include
  ${DXILCONV_PROJECT_BINARY_DIR}/include
)

macro(add_dxilconv_project_library name)
  add_llvm_library(${name} ${ARGN})
#  add_definitions(/D_ITERATOR_DEBUG_LEVEL=0)
  set_output_directory(${name} ${LLVM_RUNTIME_OUTPUT_INTDIR} ${LLVM_LIBRARY_OUTPUT_INTDIR})  
  set_target_properties(${name} PROPERTIES FOLDER "Dxilconv libraries")
endmacro(add_dxilconv_project_library)

macro(add_dxilconv_project_executable name)
  add_llvm_executable(${name} ${ARGN})
  set_target_properties(${name} PROPERTIES FOLDER "Dxilconv executables")
endmacro(add_dxilconv_project_executable)

macro(add_dxilconv_project_test_library name)
  add_dxilconv_project_library(${name} ${ARGN})
  set_target_properties(${name} PROPERTIES FOLDER "Dxilconv tests")
endmacro(add_dxilconv_project_test_library)


if(WIN32)
 add_subdirectory(lib)
 add_subdirectory(tools)
 add_subdirectory(unittests)
endif()