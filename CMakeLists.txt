cmake_minimum_required(VERSION 3.5)

project(test_mocking_utils)

# Default to C11
if(NOT CMAKE_C_STANDARD)
  set(CMAKE_C_STANDARD 11)
endif()
# Default to C++14
if(NOT CMAKE_CXX_STANDARD)
  set(CMAKE_CXX_STANDARD 14)
endif()

find_package(ament_cmake_ros REQUIRED)
find_package(mimick REQUIRED)
find_package(mimick_vendor REQUIRED)
find_package(rcutils REQUIRED)


add_library(${PROJECT_NAME} INTERFACE)
ament_target_dependencies(${PROJECT_NAME} INTERFACE rcutils mimick mimick_vendor)
target_include_directories(${PROJECT_NAME} INTERFACE include)
target_link_libraries(${PROJECT_NAME} INTERFACE mimick)

ament_export_dependencies(ament_cmake rcutils mimick_vendor)
ament_export_include_directories(include)

if(BUILD_TESTING)
  find_package(ament_lint_auto REQUIRED)
  ament_lint_auto_find_test_dependencies()
endif()

ament_package()

install(
  DIRECTORY include/
  DESTINATION include)

install(TARGETS ${PROJECT_NAME} EXPORT ${PROJECT_NAME}
  ARCHIVE DESTINATION lib
  LIBRARY DESTINATION lib
  RUNTIME DESTINATION bin)
