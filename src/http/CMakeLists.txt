
include(FindThreads)
include(FindProtobuf)
protobuf_generate_cpp(PROTO_SRC PROTO_HEADER http.proto)
# include PROTO_HEADER
include_directories(${CMAKE_CURRENT_BINARY_DIR})

carbin_cc_binary(
        NAMESPACE  melon
        NAME http_client
        SOURCES http_client.cc
        PUBLIC_LINKED_TARGETS ${CARBIN_DYLINK} ${DYNAMIC_LIB}
        PRIVATE_COMPILE_OPTIONS ${CARBIN_DEFAULT_COPTS}
        PUBLIC
)

carbin_cc_binary(
        NAMESPACE  melon
        NAME http_server
        SOURCES http_server.cc ${PROTO_SRC} ${PROTO_HEADER}
        PUBLIC_LINKED_TARGETS ${CARBIN_DYLINK} ${DYNAMIC_LIB}
        PRIVATE_COMPILE_OPTIONS ${CARBIN_DEFAULT_COPTS}
        PUBLIC
)

carbin_cc_binary(
        NAMESPACE  melon
        NAME benchmark_http
        SOURCES benchmark_http.cc
        PUBLIC_LINKED_TARGETS ${CARBIN_DYLINK} ${DYNAMIC_LIB}
        PRIVATE_COMPILE_OPTIONS ${CARBIN_DEFAULT_COPTS}
        PUBLIC
)

file(COPY key.pem
     DESTINATION ${CMAKE_CURRENT_BINARY_DIR})
file(COPY cert.pem
     DESTINATION ${CMAKE_CURRENT_BINARY_DIR})
