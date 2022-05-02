option(ENABLE_CEREAL "Enable cereal" ${ENABLE_LIBRARIES})

if (NOT ENABLE_CEREAL)
    message(STATUS "Not using cereal")
    return()
endif()

set (LIBRARY_DIR "${ClickHouse_SOURCE_DIR}/contrib/cereal")

set (SRCS
    #  "${LIBRARY_DIR}/include/armadillo"
    # "${LIBRARY_DIR}/src/mlpack/methods/linear_regression/linear_regression.cpp"
    # "${LIBRARY_DIR}/src/mlpack/methods/linear_regression/linear_regression_main.cpp"
    # "${LIBRARY_DIR}/src/mlpack/methods/linear_regression/linear_regression_train_main.cpp"
)

set (HDRS 
    "${LIBRARY_DIR}/include/cereal/archives/binary.hpp"
    # "${LIBRARY_DIR}/src/mlpack/methods/linear_regression/linear_regression.hpp"
    # "${LIBRARY_DIR}/src/mlpack/prereqs.hpp"
)

add_library(_cereal ${SRCS} ${HDRS})

target_include_directories(_cereal SYSTEM BEFORE PUBLIC "${LIBRARY_DIR}/include" "${LIBRARY_DIR}") 

add_library(ch_contrib::cereal ALIAS _cereal)