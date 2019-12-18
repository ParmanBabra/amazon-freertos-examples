cmake_minimum_required(VERSION 3.13)

project(freertos_examples)

add_executable(my_app src/main.c)

# Tell IDF build to link against this target.
set(IDF_PROJECT_EXECUTABLE my_app)

# Add some extra components. IDF_EXTRA_COMPONENT_DIRS is an variable used by ESP-IDF
# to collect extra components.
get_filename_component(
    EXTRA_COMPONENT_DIRS
    "components/foo" ABSOLUTE
)
list(APPEND IDF_EXTRA_COMPONENT_DIRS ${EXTRA_COMPONENT_DIRS})

# Override the configurations for Amazon FreeRTOS.
include_directories(BEFORE amazon-freertos-configs)

# Add amazon freertos as a subdirectory. AFR_BOARD tells which board to target.
set(AFR_BOARD espressif.esp32_devkitc CACHE INTERNAL "")
add_subdirectory(amazon-freertos)

# Link against the mqtt library so that we can use it. Dependencies are transitively
# linked.
target_link_libraries(my_app PRIVATE AFR::common)
target_link_libraries(my_app PRIVATE AFR::dev_mode_key_provisioning)
target_link_libraries(my_app PRIVATE AFR::wifi)
target_link_libraries(my_app PRIVATE AFR::mqtt)
target_link_libraries(my_app PRIVATE AFR::ble)
target_link_libraries(my_app PRIVATE AFR::ble_hal)
target_link_libraries(my_app PRIVATE AFR::ble_wifi_provisioning)
target_link_libraries(my_app PRIVATE AFR::freertos_plus_tcp)
target_link_libraries(my_app PRIVATE AFR::greengrass)
target_link_libraries(my_app PRIVATE AFR::https)
target_link_libraries(my_app PRIVATE AFR::ota)
target_link_libraries(my_app PRIVATE AFR::pkcs11)
target_link_libraries(my_app PRIVATE AFR::pkcs11_implementation)
target_link_libraries(my_app PRIVATE AFR::platform)
target_link_libraries(my_app PRIVATE AFR::secure_sockets)
target_link_libraries(my_app PRIVATE AFR::serializer)
target_link_libraries(my_app PRIVATE AFR::shadow)
target_link_libraries(my_app PRIVATE AFR::tls)
target_link_libraries(my_app PRIVATE AFR::wifi)
target_link_libraries(my_app PRIVATE AFR::crypto)
target_link_libraries(my_app PRIVATE AFR::defender)


