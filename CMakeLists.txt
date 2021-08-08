cmake_minimum_required(VERSION 3.16)

project(Adafruit_Userspace_PiTFT)

set (CMAKE_C_FLAGS "${CMAKE_C_FLAGS} -Ofast -fomit-frame-pointer")

include_directories(
    /opt/vc/include
    /opt/vc/include/interface/vcos/pthreads
    /opt/vc/include/interface/vmcs_host
    /opt/vc/include/interface/vmcs_host/linux
)

link_directories(
    /opt/vc/lib
)

add_executable(nanoscreen nanoscreen.c)
target_link_libraries(nanoscreen bcm_host)
install(TARGETS nanoscreen RUNTIME DESTINATION bin)
install(FILES nanoscreen.service DESTINATION lib/systemd/system)

add_executable(square square.c)
target_link_libraries(square bcm_host)
install(TARGETS square RUNTIME DESTINATION bin)
install(FILES square.service DESTINATION lib/systemd/system)

add_executable(tftcp tftcp.c)
target_link_libraries(tftcp bcm_host)
install(TARGETS tftcp RUNTIME DESTINATION bin)
install(FILES tftcp.service DESTINATION lib/systemd/system)
