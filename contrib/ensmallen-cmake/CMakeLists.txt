option(ENABLE_ENSMALLEN "Enable ensmallen" ${ENABLE_LIBRARIES})

if (NOT ENABLE_ENSMALLEN)
    message(STATUS "Not using ensmallen")
    return()
endif()

set (LIBRARY_DIR "${ClickHouse_SOURCE_DIR}/contrib/ensmallen")

set (SRCS
    # "${LIBRARY_DIR}/src/mlpack/methods/linear_regression/linear_regression_predict_main.cpp"
    # "${LIBRARY_DIR}/src/mlpack/methods/linear_regression/linear_regression.cpp"
    # "${LIBRARY_DIR}/src/mlpack/methods/linear_regression/linear_regression_main.cpp"
    # "${LIBRARY_DIR}/src/mlpack/methods/linear_regression/linear_regression_train_main.cpp"
)

set (HDRS 
    "${LIBRARY_DIR}/include/ensmallen.hpp"
    # "${LIBRARY_DIR}/src/mlpack/prereqs.hpp"
    # "${LIBRARY_DIR}/src/mlpack/core/util/arma_config_check.hpp"
    # "${LIBRARY_DIR}/src/mlpack/core/data/load_model_impl.hpp"
    # "${LIBRARY_DIR}/src/mlpack/core/data/save_impl.hpp"
    # "${LIBRARY_DIR}/src/mlpack/methods/logistic_regression/logistic_regression.hpp"
    # "${LIBRARY_DIR}/src/mlpack/methods/logistic_regression/logistic_regression_impl.hpp"
)

add_library(_ensmallen ${SRCS} ${HDRS})

#target_link_libraries(_ensmallen PUBLIC ch_contrib::armadillo ch_contrib::cereal _boost_headers_only)

target_include_directories(_ensmallen SYSTEM BEFORE PUBLIC "${LIBRARY_DIR}/include" "${LIBRARY_DIR}" ) 

add_library(ch_contrib::ensmallen ALIAS _ensmallen)
