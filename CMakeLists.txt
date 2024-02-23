include_directories(/usr/local/include/e2sim)
link_directories(/usr/local/lib)
link_libraries(e2sim)

find_external_library(
    DEPENDENCY_NAME e2sim
    HEADER_NAMES e2sim.h
    LIBRARY_NAME e2sim
    SEARCH_PATHS /usr/local/include
)

if(${e2sim_FOUND})
    include_directories(${e2sim_INCLUDE_DIRS})
    link_libraries(${e2sim_LIBRARIES})
    build_lib(
    LIBNAME e2sim
    LIBRARIES_TO_LINK ${e2sim_LIBRARIES}
)
endif()

build_lib(
    LIBNAME oran-interface
    SOURCE_FILES
        model/oran-interface.cc
        model/asn1c-types.cc
        model/function-description.cc
        model/kpm-indication.cc
        model/kpm-function-description.cc
        model/ric-control-message.cc
        model/ric-control-function-description.cc
        helper/oran-interface-helper.cc
        helper/indication-message-helper.cc
        helper/lte-indication-message-helper.cc
        helper/mmwave-indication-message-helper.cc
    HEADER_FILES
        model/oran-interface.h
        model/asn1c-types.h
        model/function-description.h
        model/kpm-indication.h
        model/kpm-function-description.h
        model/ric-control-message.h
        model/ric-control-function-description.h
        helper/oran-interface-helper.h
        helper/indication-message-helper.h
        helper/lte-indication-message-helper.h
        helper/mmwave-indication-message-helper.h
    LIBRARIES_TO_LINK 
        ${libcore}
        ${libe2sim}
    TEST_SOURCES
        test/oran-interface-test-suite.cc
)