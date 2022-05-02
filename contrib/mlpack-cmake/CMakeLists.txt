option(ENABLE_MLPACK "Enable mlpack" ${ENABLE_LIBRARIES})

if (NOT ENABLE_MLPACK)
    message(STATUS "Not using mlpack")
    return()
endif()

set (LIBRARY_DIR "${ClickHouse_SOURCE_DIR}/contrib/mlpack")

set (SRCS
    # "${LIBRARY_DIR}/src/mlpack/methods/linear_regression/linear_regression_predict_main.cpp"
    "${LIBRARY_DIR}/src/mlpack/methods/linear_regression/linear_regression.cpp"
    # "${LIBRARY_DIR}/src/mlpack/methods/linear_regression/linear_regression_main.cpp"
    # "${LIBRARY_DIR}/src/mlpack/methods/linear_regression/linear_regression_train_main.cpp"
)

set (HDRS 
    "${LIBRARY_DIR}/src/mlpack/methods/linear_regression/linear_regression.hpp"
    "${LIBRARY_DIR}/src/mlpack/prereqs.hpp"
    "${LIBRARY_DIR}/src/mlpack/core/util/arma_config_check.hpp"
    "${LIBRARY_DIR}/src/mlpack/core/data/load_model_impl.hpp"
    "${LIBRARY_DIR}/src/mlpack/core/data/save_impl.hpp"
    "${LIBRARY_DIR}/src/mlpack/methods/logistic_regression/logistic_regression.hpp"
    "${LIBRARY_DIR}/src/mlpack/methods/logistic_regression/logistic_regression_impl.hpp"
)

add_library(_mlpack ${SRCS} ${HDRS})

target_link_libraries(_mlpack PUBLIC ch_contrib::armadillo ch_contrib::cereal ch_contrib::ensmallen _boost_headers_only)

# include(GenerateExportHeader)
# generate_export_header(_mlpack EXPORT_FILE_NAME mlpack_export.hpp)

target_include_directories(_mlpack SYSTEM BEFORE PUBLIC "${LIBRARY_DIR}/src" "${LIBRARY_DIR}" ) 
set_target_properties(_mlpack PROPERTIES COMPILE_FLAGS
      -DBINDING_TYPE=BINDING_TYPE_CLI)

add_library(ch_contrib::mlpack ALIAS _mlpack)
