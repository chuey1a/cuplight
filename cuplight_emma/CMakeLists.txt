#Specify min version
cmake_minimum_required(VERSION 3.19)

#Include CMAKE IMPORT FILE
include(pico_sdk_import.cmake)
include(pico_extras_import.cmake)

project(cuplight_emma_project)

#init the sdk
pico_sdk_init()
if (TARGET tinyusb_device)
    #Create executable target from a source file
    add_executable(cuplight
        cuplight.c
    )
    pico_enable_stdio_usb(cuplight 1)
    pico_enable_stdio_uart(cuplight 0)


    #Specify libraries to include
    target_link_libraries(cuplight pico_stdlib hardware_sleep hardware_rtc)
    target_link_libraries(cuplight hardware_pwm hardware_gpio)
    target_link_libraries(cuplight hardware_clocks)

    #Generate all file formats
    pico_add_extra_outputs(cuplight)
elseif(PICO_ON_DEVICE)
    message(WARNING "not building hello_usb because TinyUSB submodule is not initialized in the SDK")
endif()
