cmake_minimum_required(VERSION 3.13)

project(my_app)

file(GLOB SOURCES 
    "*.c" ABSOLUTE 
    # "amazon-freertos/libraries/freertos_plus/standard/utils/src/iot_system_init.c"
    )
file(GLOB HEADERS 
    "/config_files/*.h" ABSOLUTE
)

add_executable(my_app ${SOURCES} ${HEADERS})
set(IDF_PROJECT_EXECUTABLE my_app)

# Add some external components to the project
get_filename_component(EXTRA_COMPONENT_DIRS
    "components/foo" ABSOLUTE
)
set(IDF_EXTRA_COMPONENT_DIRS ${EXTRA_COMPONENT_DIRS})
set(IDF_SDKCONFIG_DEFAULTS "${CMAKE_CURRENT_LIST_DIR}/sdkconfig.defaults")

set(AFR_BOARD espressif.esp32_devkitc CACHE INTERNAL "")
add_subdirectory(amazon-freertos)

target_link_libraries(my_app PRIVATE AFR::demo_base)
target_link_libraries(my_app PRIVATE AFR::demo_ble_numeric_comparison)
target_link_libraries(my_app PRIVATE AFR::ble)
target_link_libraries(my_app PRIVATE AFR::ble_hal)
target_link_libraries(my_app PRIVATE AFR::ble_wifi_provisioning)
target_link_libraries(my_app PRIVATE AFR::common)
target_link_libraries(my_app PRIVATE AFR::crypto)
target_link_libraries(my_app PRIVATE AFR::defender)
target_link_libraries(my_app PRIVATE AFR::dev_mode_key_provisioning)
target_link_libraries(my_app PRIVATE AFR::freertos_plus_tcp)
target_link_libraries(my_app PRIVATE AFR::greengrass)
target_link_libraries(my_app PRIVATE AFR::https)
target_link_libraries(my_app PRIVATE AFR::kernel)
target_link_libraries(my_app PRIVATE AFR::mqtt)
target_link_libraries(my_app PRIVATE AFR::ota)
target_link_libraries(my_app PRIVATE AFR::pkcs11)
target_link_libraries(my_app PRIVATE AFR::pkcs11_implementation)
target_link_libraries(my_app PRIVATE AFR::platform)
target_link_libraries(my_app PRIVATE AFR::secure_sockets)
target_link_libraries(my_app PRIVATE AFR::serializer)
target_link_libraries(my_app PRIVATE AFR::shadow)
target_link_libraries(my_app PRIVATE AFR::tls)
target_link_libraries(my_app PRIVATE AFR::wifi)