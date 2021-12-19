idf_component_register(REQUIRES arduino)
get_target_property(ARDUINO_SOURCE_DIR __idf_arduino SOURCE_DIR)
add_custom_target(ota ALL DEPENDS gen_project_binary)
add_custom_command(
        TARGET ota
        COMMAND ${ARDUINO_SOURCE_DIR}/tools/espota.py -r -i ${CONFIG_ARDUINOOTA_TARGET_ADDRESS} -P ${CONFIG_ARDUINOOTA_TARGET_PORT} -p ${CONFIG_ARDUINOOTA_HOST_PORT} --auth= -f ${CMAKE_BINARY_DIR}/${CMAKE_PROJECT_NAME}.bin
        DEPENDS ${PROJECT_BINARY_DIR}/${mihau-temp}.bin
        USES_TERMINAL
)