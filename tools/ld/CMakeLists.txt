configure_file(${CMAKE_CURRENT_SOURCE_DIR}/eosio-ld.cpp.in ${CMAKE_BINARY_DIR}/icbs-ld.cpp)

add_tool(icbs-ld)
