find_package(Boost REQUIRED COMPONENTS filesystem program_options system)

add_library(boost INTERFACE IMPORTED)
set_target_properties(boost PROPERTIES
  INTERFACE_INCLUDE_DIRECTORIES "${Boost_INCLUDE_DIRS}"
  INTERFACE_LINK_LIBRARIES "${Boost_LIBRARIES}")

add_executable(deltille_detector DeltilleDetector.cpp)
target_link_libraries(deltille_detector deltille boost)

add_executable(main main.cpp)
target_link_libraries(main deltille boost)

add_executable(ch_test charuco_test.cpp)
target_link_libraries(ch_test deltille boost)

add_executable(board_detect board_detect.cpp)
target_link_libraries(board_detect deltille)

add_executable(board_detect_v board_detect_video.cpp)
target_link_libraries(board_detect_v deltille)

install(TARGETS deltille_detector DESTINATION ${CMAKE_INSTALL_BINDIR})
