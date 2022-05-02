option(ENABLE_ARMADILLO "Enable armadillo" ${ENABLE_LIBRARIES})

if (NOT ENABLE_ARMADILLO)
    message(STATUS "Not using armadillo")
    return()
endif()

set (LIBRARY_DIR "${ClickHouse_SOURCE_DIR}/contrib/armadillo-code")

set (SRCS
     "${LIBRARY_DIR}/include/armadillo"
    # "${LIBRARY_DIR}/src/mlpack/methods/linear_regression/linear_regression.cpp"
    # "${LIBRARY_DIR}/src/mlpack/methods/linear_regression/linear_regression_main.cpp"
    # "${LIBRARY_DIR}/src/mlpack/methods/linear_regression/linear_regression_train_main.cpp"
)

# set (HDRS 
#     "${LIBRARY_DIR}/include/armadillo_bits/arma_config.hpp"
#     "${LIBRARY_DIR}/include/armadillo_bits/typedef_elem.hpp"
#     # "${LIBRARY_DIR}/src/mlpack/methods/linear_regression/linear_regression.hpp"
#     # "${LIBRARY_DIR}/src/mlpack/prereqs.hpp"
# )

add_library(_armadillo ${SRCS})

target_include_directories(_armadillo SYSTEM BEFORE PUBLIC "${LIBRARY_DIR}/include" "${LIBRARY_DIR}" "${LIBRARY_DIR}/tmp/include/armadillo_bits") 
target_include_directories(_armadillo SYSTEM BEFORE PUBLIC "${LIBRARY_DIR}/include/armadillo_bits") 
target_include_directories(_armadillo PRIVATE common)
add_library(ch_contrib::armadillo ALIAS _armadillo)