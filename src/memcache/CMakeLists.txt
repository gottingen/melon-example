
include(FindThreads)
include(FindProtobuf)
#protobuf_generate_cpp(PROTO_SRC PROTO_HEADER echo.proto)
# include PROTO_HEADER
include_directories(${CMAKE_CURRENT_BINARY_DIR})

carbin_cc_binary(
        NAMESPACE melon
        NAME memcache_client
        SOURCES client.cc ${PROTO_SRC}
        PUBLIC_LINKED_TARGETS ${CARBIN_DYLINK} ${DYNAMIC_LIB}
        PRIVATE_COMPILE_OPTIONS ${CARBIN_DEFAULT_COPTS}
        PUBLIC
)
