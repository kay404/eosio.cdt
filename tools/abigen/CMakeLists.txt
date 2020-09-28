configure_file(${CMAKE_CURRENT_SOURCE_DIR}/eosio-abigen.cpp.in ${CMAKE_BINARY_DIR}/icbs-abigen.cpp)

add_tool(icbs-abigen)
