file(GLOB HEADERS "*.hpp"
                  "*.h")

add_library(icbs
            eosiolib.cpp
            crypto.cpp
            ${HEADERS})

add_library(icbs_malloc
            malloc.cpp
            ${HEADERS})

add_library(icbs_dsm
            simple_malloc.cpp
            ${HEADERS})

add_library(icbs_cmem
            memory.cpp
            ${HEADERS})

add_native_library(native_icbs
                   eosiolib.cpp
                   crypto.cpp
                   malloc.cpp
                   ${HEADERS})

set_target_properties(icbs_malloc PROPERTIES LINKER_LANGUAGE C)

target_include_directories(icbs PUBLIC
                                 ${CMAKE_SOURCE_DIR}/libc/musl/include
                                 ${CMAKE_SOURCE_DIR}/libc/musl/src/internal
                                 ${CMAKE_SOURCE_DIR}/libc/musl/src/crypt
                                 ${CMAKE_SOURCE_DIR}/libc/musl/arch/eos
                                 ${CMAKE_SOURCE_DIR}/libcxx/include
                                 ${CMAKE_SOURCE_DIR}
                                 ${CMAKE_SOURCE_DIR}/boost/include)

target_link_libraries( icbs c c++ )
add_dependencies( native_icbs icbs )

add_custom_command( TARGET icbs POST_BUILD COMMAND ${CMAKE_COMMAND} -E copy $<TARGET_FILE:icbs> ${BASE_BINARY_DIR}/lib )
add_custom_command( TARGET icbs_malloc POST_BUILD COMMAND ${CMAKE_COMMAND} -E copy $<TARGET_FILE:icbs_malloc> ${BASE_BINARY_DIR}/lib )
add_custom_command( TARGET icbs_dsm POST_BUILD COMMAND ${CMAKE_COMMAND} -E copy $<TARGET_FILE:icbs_dsm> ${BASE_BINARY_DIR}/lib )
add_custom_command( TARGET icbs_cmem POST_BUILD COMMAND ${CMAKE_COMMAND} -E copy $<TARGET_FILE:icbs_cmem> ${BASE_BINARY_DIR}/lib )
add_custom_command( TARGET native_icbs POST_BUILD COMMAND ${CMAKE_COMMAND} -E copy $<TARGET_FILE:native_icbs> ${BASE_BINARY_DIR}/lib )

file(COPY ${CMAKE_CURRENT_SOURCE_DIR}/../eosiolib DESTINATION ${BASE_BINARY_DIR}/include FILES_MATCHING PATTERN "*.h" PATTERN "*.hpp")
