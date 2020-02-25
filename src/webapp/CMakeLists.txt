#Zero9 Small Simple Web UI
add_executable(zero_9small_webapp zero_9small_webapp.cpp)

target_link_libraries(zero_9small_webapp "${TORCH_LIBRARIES}")
set_property(TARGET zero_9small_webapp PROPERTY CXX_STANDARD 17)

if (MSVC)
  file(GLOB TORCH_DLLS "${TORCH_INSTALL_PREFIX}/lib/*.dll")
  add_custom_command(TARGET zero_9small_webapp
    POST_BUILD
    COMMAND ${CMAKE_COMMAND} -E copy_if_different
    ${TORCH_DLLS}
    $<TARGET_FILE_DIR:zero_9small_webapp>)
endif(MSVC)

target_link_libraries(zero_9small_webapp rapidjson)
target_link_libraries(zero_9small_webapp util)
target_link_libraries(zero_9small_webapp rgen)
target_link_libraries(zero_9small_webapp distributions)
target_link_libraries(zero_9small_webapp pytorch_util)
target_link_libraries(zero_9small_webapp game)
target_link_libraries(zero_9small_webapp encoders)
target_link_libraries(zero_9small_webapp experience)
target_link_libraries(zero_9small_webapp models)
target_link_libraries(zero_9small_webapp agents)
target_link_libraries(zero_9small_webapp Boost::program_options)
target_link_libraries(zero_9small_webapp wt Wt::HTTP)
