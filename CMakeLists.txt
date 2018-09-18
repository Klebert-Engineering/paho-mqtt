cmake_minimum_required (VERSION 3.5.0 FATAL_ERROR)
project (paho-mqtt)
add_library (${PROJECT_NAME} SHARED IMPORTED GLOBAL)

if (WIN32)
  if (CMAKE_SIZEOF_VOID_P EQUAL 8)
    set (paho_mqtt_base_dir ${CMAKE_CURRENT_SOURCE_DIR}/msvc2015_x64)
    set_target_properties (${PROJECT_NAME}
        PROPERTIES
        IMPORTED_LOCATION ${paho_mqtt_base_dir}/lib/paho-mqtt3a.dll
        IMPORTED_IMPLIB ${paho_mqtt_base_dir}/lib/paho-mqtt3a.lib
        INTERFACE_INCLUDE_DIRECTORIES ${paho_mqtt_base_dir}/include
    )
    configure_file(${paho_mqtt_base_dir}/lib/paho-mqtt3a.dll ${CMAKE_RUNTIME_OUTPUT_DIRECTORY} COPYONLY)
  else()
    message(FATAL_ERROR "32bit version of the paho lib is not present.")
  endif()
else () 
    message(FATAL_ERROR "Platform not yet supported.")
endif ()
