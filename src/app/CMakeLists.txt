add_executable(zero_9small_selfplay zero_9small_selfplay.cpp)

find_package(Torch REQUIRED)
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} ${TORCH_CXX_FLAGS}")

target_link_libraries(zero_9small_selfplay "${TORCH_LIBRARIES}")
set_property(TARGET zero_9small_selfplay PROPERTY CXX_STANDARD 17)

if (MSVC)
  file(GLOB TORCH_DLLS "${TORCH_INSTALL_PREFIX}/lib/*.dll")
  add_custom_command(TARGET zero_9small_selfplay
    POST_BUILD
    COMMAND ${CMAKE_COMMAND} -E copy_if_different
    ${TORCH_DLLS}
    $<TARGET_FILE_DIR:zero_9small_selfplay>)
endif(MSVC)

target_link_libraries(zero_9small_selfplay rapidjson)
target_link_libraries(zero_9small_selfplay util)
target_link_libraries(zero_9small_selfplay rgen)
target_link_libraries(zero_9small_selfplay distributions)
target_link_libraries(zero_9small_selfplay pytorch_util)
target_link_libraries(zero_9small_selfplay game)
target_link_libraries(zero_9small_selfplay encoders)
target_link_libraries(zero_9small_selfplay experience)
target_link_libraries(zero_9small_selfplay models)
target_link_libraries(zero_9small_selfplay agents)
