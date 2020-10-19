set(CMAKE_ARCHIVE_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/bin)
set(CMAKE_LIBRARY_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/bin)
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/bin)

include_directories(${CMAKE_CURRENT_BINARY_DIR})
include_directories(${CMAKE_CURRENT_SOURCE_DIR}/include)
include_directories(${Boost_INCLUDE_DIR})
link_directories(${Boost_LIBRARY_DIRS})

add_library(PSTREAMS INTERFACE)
target_include_directories(PSTREAMS INTERFACE ${PSTREAMS_FOLDER_PATH})

add_library(JSON INTERFACE)
target_include_directories(JSON INTERFACE ${NLOHMANN_JSON_FOLDER})
add_executable(${PROJECT_NAME} main.cc)
target_link_libraries(${PROJECT_NAME} fmt::fmt JSON PSTREAMS)

target_include_directories(${PROJECT_NAME} PUBLIC ${PROJECT_HDRS_FOLDER})
install(TARGETS ${PROJECT_NAME} DESTINATION bin)