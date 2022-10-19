
include(FindThreads)
include(FindProtobuf)

find_path(GPERFTOOLS_INCLUDE_DIR NAMES gperftools/heap-profiler.h)
find_library(GPERFTOOLS_LIBRARIES NAMES tcmalloc_and_profiler)
include_directories(${GPERFTOOLS_INCLUDE_DIR})

set(AUX_LIB readline ncurses)

carbin_cc_binary(
        NAMESPACE melon
        NAME redis_cli
        SOURCES redis_cli.cc
        PUBLIC_LINKED_TARGETS ${CARBIN_DYLINK}  ${DYNAMIC_LIB} ${AUX_LIB}
        PRIVATE_COMPILE_OPTIONS ${CARBIN_DEFAULT_COPTS}
        PUBLIC
)

carbin_cc_binary(
        NAMESPACE melon
        NAME redis_press
        SOURCES redis_press.cc
        PUBLIC_LINKED_TARGETS ${CARBIN_DYLINK}  ${DYNAMIC_LIB}
        PRIVATE_COMPILE_OPTIONS ${CARBIN_DEFAULT_COPTS}
        PUBLIC
)

carbin_cc_binary(
        NAMESPACE melon
        NAME redis_server
        SOURCES redis_server.cc ${PROTO_SRC}
        PUBLIC_LINKED_TARGETS ${CARBIN_DYLINK}  ${DYNAMIC_LIB}
        PRIVATE_COMPILE_OPTIONS ${CARBIN_DEFAULT_COPTS}
        PUBLIC
)