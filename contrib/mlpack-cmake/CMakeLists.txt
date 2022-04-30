option(ENABLE_MLPACK "Enable mlpack" ${ENABLE_LIBRARIES})

if (NOT ENABLE_MLPACK)
    message(STATUS "Not using mlpack")
    return()
endif()

set (LIBRARY_DIR "${ClickHouse_SOURCE_DIR}/contrib/mlpack")

set (SRCS
    "${LIBRARY_DIR}/src/mlpack/methods/linear_regression/linear_regression_predict_main.cpp"
    "${LIBRARY_DIR}/src/mlpack/methods/linear_regression/linear_regression.cpp"
    "${LIBRARY_DIR}/src/mlpack/methods/linear_regression/linear_regression_main.cpp"
    "${LIBRARY_DIR}/src/mlpack/methods/linear_regression/linear_regression_train_main.cpp"
)

set (HDRS 
    "${LIBRARY_DIR}/src/mlpack/methods/linear_regression/linear_regression.hpp"
    "${LIBRARY_DIR}/src/mlpack/prereqs.hpp"
)

add_library(_mlpack ${SRCS} ${HDRS})

target_link_libraries(_mlpack PUBLIC ch_contrib::armadillo)

target_include_directories(_mlpack SYSTEM BEFORE PUBLIC "${LIBRARY_DIR}/src" "${LIBRARY_DIR}") 

add_library(ch_contrib::mlpack ALIAS _mlpack)