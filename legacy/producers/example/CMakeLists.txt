GET_FILENAME_COMPONENT(DIRNAME ${CMAKE_CURRENT_LIST_DIR} NAME)
SET(PLUGIN_NAME plugin.${DIRNAME})
SET_PROPERTY(GLOBAL APPEND PROPERTY CONVERTER_PLUGIN ${PLUGIN_NAME})

INCLUDE_DIRECTORIES(include)

SET(PLUGIN_SRC
  src/ExampleConverterPlugin.cc
  )
ADD_LIBRARY(${PLUGIN_NAME} SHARED ${PLUGIN_SRC})

SET(PRODUCER_NAME ${DIRNAME}procuder)
SET(PRODUCER_SRC
  src/ExampleProducer.cxx
  )
ADD_EXECUTABLE(${PRODUCER_NAME} ${PRODUCER_SRC})
TARGET_LINK_LIBRARIES(${PRODUCER_NAME} EUDAQ)

INSTALL(TARGETS ${PLUGIN_NAME} ${PRODUCER_NAME}
  RUNTIME DESTINATION bin
  LIBRARY DESTINATION lib
  ARCHIVE DESTINATION lib
  )
