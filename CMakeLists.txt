cmake_minimum_required(VERSION 3.5)

project(rclcs C)



find_package(ament_cmake REQUIRED)
find_package(ament_cmake_python REQUIRED)

if(NOT WIN32)
add_custom_target(rclcs ALL
	COMMAND 
	"xbuild" rclcs.csproj /property:OutputPath=${CMAKE_BINARY_DIR} /property:AssemblyName=rclcs /property:GenerateDocumentation=true /property:DocumentationFile="rclcs.xml"
	WORKING_DIRECTORY
	${CMAKE_SOURCE_DIR}/src
)
else()
add_custom_target(rclcs ALL
	COMMAND 
	"msbuild" rclcs.csproj /property:OutputPath=${CMAKE_BINARY_DIR} /property:AssemblyName=rclcs /property:Platform=x64 /property:AllowUnsafeBlocks=true /property:GenerateDocumentation=true /property:DocumentationFile="rclcs.xml"
	WORKING_DIRECTORY
	${CMAKE_SOURCE_DIR}/src
)
endif()

#ament_export_dependencies(rosidl_cmake)
#ament_export_include_directories(include)
#ament_export_libraries(${PROJECT_NAME})

#ament_python_install_package(${PROJECT_NAME})



ament_package(
  
)
if(NOT WIN32)
	install(FILES ${CMAKE_BINARY_DIR}/rclcs.dll DESTINATION lib)
	install(FILES ${CMAKE_CURRENT_SOURCE_DIR}/src/rclcs.xml DESTINATION lib)
else()
	install(FILES ${CMAKE_BINARY_DIR}/rclcs.dll DESTINATION bin)
	install(FILES ${CMAKE_CURRENT_SOURCE_DIR}/src/rclcs.xml DESTINATION bin)
endif()

#install(TARGETS rclcs.dll DESTINATION lib)
#install(
#  PROGRAMS bin/rosidl_generator_cs
#  DESTINATION lib/rosidl_generator_cs
#)

#install(
#  DIRECTORY include/
#  DESTINATION include
#)
#
#install(
#  TARGETS ${PROJECT_NAME}
#  ARCHIVE DESTINATION lib
#  LIBRARY DESTINATION lib
#  RUNTIME DESTINATION bin
#)
