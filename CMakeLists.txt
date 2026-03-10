  # generate custom msg headers
  set(LIVOX_INTERFACES livox_interfaces2)
  rosidl_generate_interfaces(${LIVOX_INTERFACES}
    "msg/CustomPoint.msg"
    "msg/CustomMsg.msg"
    DEPENDENCIES builtin_interfaces std_msgs
    LIBRARY_NAME ${PROJECT_NAME}
  )

  ...

  # Always get the C++ typesupport target for the generated interfaces and link it
  rosidl_get_typesupport_target(LIVOX_INTERFACE_TARGET
    ${LIVOX_INTERFACES} "rosidl_typesupport_cpp")

  if(LIVOX_INTERFACE_TARGET)
    target_link_libraries(${PROJECT_NAME} "${LIVOX_INTERFACE_TARGET}")
  endif()

  # include file directory
  target_include_directories(${PROJECT_NAME} PUBLIC
    ${PCL_INCLUDE_DIRS}
    ${APR_INCLUDE_DIRS}
    ${LIVOX_LIDAR_SDK_INCLUDE_DIR}
    3rdparty
    src
  )

  # link libraries
  target_link_libraries(${PROJECT_NAME}
    ${LIVOX_LIDAR_SDK_LIBRARY}
    ${PPT_LIBRARY}
    ${Boost_LIBRARY}
    ${PCL_LIBRARIES}
    ${APR_LIBRARIES}
  )
