configure_file(${CMAKE_CURRENT_SOURCE_DIR}/eosio-init.cpp ${CMAKE_BINARY_DIR}/icbs-init.cpp @ONLY)

add_tool(icbs-init)
